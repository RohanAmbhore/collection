<a href="https://stackoverflow.com/questions/35812592/electron-require-ipcrenderer-not-working">https://stackoverflow.com/questions/35812592/electron-require-ipcrenderer-not-working</a><div id="articleHeader"><h1>Electron require ipcRenderer not working</h1></div>

<p>I am trying to do a simple ipc.send and ipc.on but for some reason I am getting undefined on this electron require.</p>

<p>libs/custom-menu.js:</p>

<pre><code>'use-strict';

const BrowserWindow = require('electron').BrowserWindow;
const ipcRenderer = require('electron').ipcRenderer;

exports.getTemplate = function () {
  const template = [
    {
      label: 'Roll20',
      submenu: [
        {
          label: 'Player Handbook',
          click() {
            console.log('test');
          },
        },
      ],
    },
    {
      label: 'View',
      submenu: [
        {
          label: 'Toggle Fullscreen',
          accelerator: 'F11',
          click(item, focusedWindow) {
            if (focusedWindow) {
              focusedWindow.setFullScreen(!focusedWindow.isFullScreen());
            }
          },
        },
        {
          label: 'Toggle Developer Tools',
          accelerator: (function () {
            if (process.platform === 'darwin') {
              return 'Alt+Command+I';
            }
            return 'Ctrl+Shift+I';
          }()),
          click(item, focusedWindow) {
            if (focusedWindow) {
              focusedWindow.toggleDevTools();
            }
          },
        },
        {
          label: 'Reload',
          accelerator: 'F5',
          click() {
            BrowserWindow.getFocusedWindow().reloadIgnoringCache();
          },
        },
      ],
    },
    {
      label: 'Random Generators',
      submenu: [
        {
          label: 'World Generator',
          click() {
            ipcRenderer.send('show-world');
          },
        },
      ],
    },
  ];
  return template;
};
</code></pre>

<p>The error is 
cannot read property 'send' of undefined.</p>
    