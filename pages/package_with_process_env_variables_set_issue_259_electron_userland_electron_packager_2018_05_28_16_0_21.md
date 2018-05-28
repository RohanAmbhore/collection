<a href="https://github.com/electron-userland/electron-packager/issues/259">https://github.com/electron-userland/electron-packager/issues/259</a><div id="articleHeader"><h1>              Package with process.env variables set            #259    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/mmahalwy" target="_blank">mmahalwy</a>  opened this Issue
        <relative-time>on Feb 8, 2016</relative-time>
        · 8 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            




            

  

    



    

      


  
    
      

          <p>In my main.js file, I have <code>process.env</code> variables set that I need to package and have them set when you open the packaged app. How can I do this? Here is my package.js file:</p>
<pre><code>/* eslint strict: 0, no-shadow: 0, no-unused-vars: 0, no-console: 0 */
'use strict';

const os = require('os');
const webpack = require('webpack');
const cfg = require('./webpack/app.production.js');
const packager = require('electron-packager');
const del = require('del');
const exec = require('child_process').exec;
const argv = require('minimist')(process.argv.slice(2));
const pkg = require('./package.json');
const devDeps = Object.keys(pkg.devDependencies);

const appName = argv.name || argv.n || pkg.productName;
const shouldUseAsar = argv.asar || argv.a || false;
const shouldBuildAll = argv.all || false;

console.log(process.env.GOOGLE_APP_CLIENT);

const DEFAULT_OPTS = {
  dir: './',
  name: appName,
  asar: shouldUseAsar,
  ignore: [
    '/test($|/)',
    '/tools($|/)',
    '/release($|/)'
  ].concat(devDeps.map(name =&gt; `/node_modules/${name}($|/)`))
};

const icon = argv.icon || argv.i || 'app/app';

if (icon) {
  DEFAULT_OPTS.icon = icon;
}

const version = argv.version || argv.v;

if (version) {
  DEFAULT_OPTS.version = version;
  startPack();
} else {
  // use the same version as the currently-installed electron-prebuilt
  exec('npm list electron-prebuilt', (err, stdout) =&gt; {
    if (err) {
      DEFAULT_OPTS.version = '0.36.2';
    } else {
      DEFAULT_OPTS.version = stdout.split('electron-prebuilt@')[1].replace(/\s/g, '');
    }

    startPack();
  });
}


function startPack() {
  console.log('start pack...');
  webpack(cfg, (err, stats) =&gt; {
    if (err) return console.error(err);
    del('release')
    .then(paths =&gt; {
      if (shouldBuildAll) {
        // build for all platforms
        const archs = ['ia32', 'x64'];
        const platforms = ['linux', 'win32', 'darwin'];

        platforms.forEach(plat =&gt; {
          archs.forEach(arch =&gt; {
            pack(plat, arch, log(plat, arch));
          });
        });
      } else {
        // build for current platform only
        pack(os.platform(), os.arch(), log(os.platform(), os.arch()));
      }
    })
    .catch(err =&gt; {
      console.error(err);
    });
  });
}

function pack(plat, arch, cb) {
  // there is no darwin ia32 electron
  if (plat === 'darwin' && arch === 'ia32') return;

  const iconObj = {
    icon: DEFAULT_OPTS.icon + (() =&gt; {
      let extension = '.png';
      if (plat === 'darwin') {
        extension = '.icns';
      } else if (plat === 'win32') {
        extension = '.ico';
      }
      return extension;
    })()
  };

  const opts = Object.assign({}, DEFAULT_OPTS, iconObj, {
    platform: plat,
    arch,
    prune: true,
    out: `release/${plat}-${arch}`
  });

  packager(opts, cb);
}


function log(plat, arch) {
  return (err, filepath) =&gt; {
    if (err) return console.error(err);
    console.log(`${plat}-${arch} finished!`);
  };
}
</code></pre>
      