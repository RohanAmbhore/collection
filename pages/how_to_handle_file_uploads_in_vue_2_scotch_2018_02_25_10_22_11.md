<a href="https://scotch.io/tutorials/how-to-handle-file-uploads-in-vue-2">https://scotch.io/tutorials/how-to-handle-file-uploads-in-vue-2</a><div id="articleHeader"><h1>How to Handle File Uploads in Vue 2</h1></div>






<p>In this article, we will talk about how to handle file uploads with VueJs. We will create an images uploader that allow user to upload single or multiple images file by drag and drop or select file dialog. </p>
<p>We will then upload the selected images and display them accordingly. We will also learn to filter the upload file type, for example, we only allow images, do not allow file type like PDF.</p>
<p><div class="readableLargeImageContainer"><img src="https://cdn.scotch.io/272/9hcPMzQR7kNqz6R0cTeQ_upload-vue.gif" alt="Image uploader" /></div></p>

<h2 id="file-upload-ui-api">
    <a href="#toc-file-upload-ui-api" target="_blank">
      #
      File Upload UI & API
    </a> 
  </h2>
<p>File upload consists of two parts: <em>the UI (front-end)</em> and <em>the API (back-end)</em>. We will be using <strong>VueJs</strong> to handle the UI part. We need a backend application to accept the uploaded files. You may follow the backend tutorials or download and run either one of these server side application to handle file upload for your backend:- </p>

<p>We will be using <strong>File upload with Hapi.js</strong> as our backend throughout this articles. We will also learn the tricks to enable fake upload on the front-end.</p>
<h2 id="setup-project-with-vue-cli">
    <a href="#toc-setup-project-with-vue-cli" target="_blank">
      #
      Setup Project with Vue-Cli
    </a> 
  </h2>
<p>We will be using <a href="https://github.com/vuejs/vue-cli" target="_blank">vue-cli</a> to scaffold Vue.js projects. We will be using the <code>webpack-simple</code> project template.</p>
<pre><code># install cli
npm install vue-cli -g

# then create project, with sass
# follow the instructions to install all necessary dependencies
vue init webpack-simple file-upload-vue</code></pre>
<p>Alright, all set. Let's proceed to create our component.</p>
<h2 id="file-upload-component">
    <a href="#toc-file-upload-component" target="_blank">
      #
      File Upload Component
    </a> 
  </h2>
<p>We will write our code in <code>App.vue</code>. Remove all the auto-generated code in the file.</p>
<pre><code>&lt;!-- App.vue --&gt;

&lt;!-- HTML Template --&gt;
&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;div class="container"&gt;
      &lt;!--UPLOAD--&gt;
      &lt;form enctype="multipart/form-data" novalidate v-if="isInitial || isSaving"&gt;
        &lt;h1&gt;Upload images&lt;/h1&gt;
        &lt;div class="dropbox"&gt;
          &lt;input type="file" multiple :name="uploadFieldName" :disabled="isSaving" @change="filesChange($event.target.name, $event.target.files); fileCount = $event.target.files.length"
            accept="image/*" class="input-file"&gt;
            &lt;p v-if="isInitial"&gt;
              Drag your file(s) here to begin&lt;br&gt; or click to browse
            &lt;/p&gt;
            &lt;p v-if="isSaving"&gt;
              Uploading {{ fileCount }} files...
            &lt;/p&gt;
        &lt;/div&gt;
      &lt;/form&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;!-- Javascript --&gt;
&lt;script&gt;
&lt;/script&gt;

&lt;!-- SASS styling --&gt;
&lt;style lang="scss"&gt;
&lt;/style&gt;</code></pre>
<p>Notes:-</p>
<ol>
<li>Our <code>App.vue</code> component consists of 3 part: template (HTML), script (Javascript) and styles (SASS).</li>
<li>Our template has an upload form.</li>
<li>The form attribute <code>enctype="multipart/form-data"</code> is important. To enable file upload, this attribute must be set. Learn more about enctype <a href="https://www.w3schools.com/tags/att_form_enctype.asp" target="_blank">here</a>.</li>
<li>We have a file input <code>&lt;input type="file" /&gt;</code> to accept file upload. The property <code>multiple</code> indicate it's allow multiple file upload. Remove it for single file upload.</li>
<li>We will handle the file input <code>change</code> event. Whenever the file input change (someone drop or select files), we will trigger the <code>filesChange</code> function and pass in the control name and selected files <code>$event.target.files</code>, and then upload to server.</li>
<li>We limit the file input to accept images only with the attribute <code>accept="image/*"</code>.</li>
<li>The file input will be disabled during upload, so user can only drop / select files again after upload complete.</li>
<li>We capture the <code>fileCount</code> of the when file changes. We use the <code>fileCount</code> variable in displaying number of files uploading <code>Uploading {{ fileCount }} files...</code>.</li>
</ol>
<h2 id="style-our-file-upload-component">
    <a href="#toc-style-our-file-upload-component" target="_blank">
      #
      Style our File Upload Component
    </a> 
  </h2>
<p>Now, that's the interesting part. Currently, our component look like this:</p><div>Related Course: <a href="https://bit.ly/2gCILn1" target="_blank">Build an Online Shop with Vue</a></div>
<p><div class="readableLargeImageContainer"><img src="https://cdn.scotch.io/272/sMqdStyLSAeWbAhjIErP_Screen%20Shot%202017-02-11%20at%2011.30.10%20AM.png" alt="File upload component without styling" /></div></p>
<p>We need to transform it to look like this:</p>
<p><div class="readableLargeImageContainer"><img src="https://cdn.scotch.io/272/qwyQjaccRiSzkjIAadKL_Screen%20Shot%202017-02-11%20at%2011.33.19%20AM.png" alt="File upload component with styling" /></div></p>
<p>Let's style it!</p>
<pre><code>&lt;!-- App.vue --&gt;
...

&lt;!-- SASS styling --&gt;
&lt;style lang="scss"&gt;
  .dropbox {
    outline: 2px dashed grey; /* the dash box */
    outline-offset: -10px;
    background: lightcyan;
    color: dimgray;
    padding: 10px 10px;
    min-height: 200px; /* minimum height */
    position: relative;
    cursor: pointer;
  }

  .input-file {
    opacity: 0; /* invisible but it's there! */
    width: 100%;
    height: 200px;
    position: absolute;
    cursor: pointer;
  }

  .dropbox:hover {
    background: lightblue; /* when mouse over to the drop zone, change color */
  }

  .dropbox p {
    font-size: 1.2em;
    text-align: center;
    padding: 50px 0;
  }
&lt;/style&gt;</code></pre>
<p>With only few lines of scss, our component looks prettier now.</p>
<p>Notes:-</p>
<ol>
<li>We make the file input invisible by applying <code>opacity: 0</code> style. This doesn't hide the file input, it just make it invisible.</li>
<li>Then, we style the file input parent element, the <code>dropbox</code> css class. We make it look like a drop file zone surround with dash.</li>
<li>Then, we align the text inside dropbox to center.</li>
</ol>
<h2 id="file-upload-component-code">
    <a href="#toc-file-upload-component-code" target="_blank">
      #
      File Upload Component Code
    </a> 
  </h2>
<p>Let's proceed to code our component.</p>
<pre><code>&lt;!-- App.vue --&gt;
...

&lt;!-- Javascript --&gt;
&lt;script&gt;
  import { upload } from './file-upload.service';

  const STATUS_INITIAL = 0, STATUS_SAVING = 1, STATUS_SUCCESS = 2, STATUS_FAILED = 3;

  export default {
    name: 'app',
    data() {
      return {
        uploadedFiles: [],
        uploadError: null,
        currentStatus: null,
        uploadFieldName: 'photos'
      }
    },
    computed: {
      isInitial() {
        return this.currentStatus === STATUS_INITIAL;
      },
      isSaving() {
        return this.currentStatus === STATUS_SAVING;
      },
      isSuccess() {
        return this.currentStatus === STATUS_SUCCESS;
      },
      isFailed() {
        return this.currentStatus === STATUS_FAILED;
      }
    },
    methods: {
      reset() {
        // reset form to initial state
        this.currentStatus = STATUS_INITIAL;
        this.uploadedFiles = [];
        this.uploadError = null;
      },
      save(formData) {
        // upload data to the server
        this.currentStatus = STATUS_SAVING;

        upload(formData)
          .then(x =&gt; {
            this.uploadedFiles = [].concat(x);
            this.currentStatus = STATUS_SUCCESS;
          })
          .catch(err =&gt; {
            this.uploadError = err.response;
            this.currentStatus = STATUS_FAILED;
          });
      },
      filesChange(fieldName, fileList) {
        // handle file changes
        const formData = new FormData();

        if (!fileList.length) return;

        // append the files to FormData
        Array
          .from(Array(fileList.length).keys())
          .map(x =&gt; {
            formData.append(fieldName, fileList[x], fileList[x].name);
          });

        // save it
        this.save(formData);
      }
    },
    mounted() {
      this.reset();
    },
  }

&lt;/script&gt;</code></pre>
<p>Notes:-</p>
<ol>
<li>Our component will have a few statuses: STATUS_INITIAL, STATUS_SAVING, STATUS_SUCCESS, STATUS_FAILED, the variable name is pretty expressive themselves.</li>
<li>Later on, we will call the <a href="https://github.com/chybie/file-upload-hapi" target="_blank">Hapi.js file upload</a> API to upload images, the API accept a field call <code>photos</code>. That's our file input field name. </li>
<li>We handle the file changes with the <code>filesChange</code> function. <code>FileList</code> is an object returned by the files property of the HTML  element. It allow us to access the list of files selected with the  element. Learn more [here]((<a href="https://developer.mozilla.org/en/docs/Web/API/FileList" target="_blank">https://developer.mozilla.org/en/docs/Web/API/FileList</a>).</li>
<li>We then create a new <code>FormData</code>, and append all our <code>photos</code> files to it. <code>FormData</code> interface provides a way to easily construct a set of key/value pairs representing form fields and their values. Learn more <a href="https://developer.mozilla.org/en/docs/Web/API/FormData" target="_blank">here</a>.</li>
<li>The <code>save</code> function will call our file upload service (hang on, we will create the service next!). We also set the status according to the result. </li>
<li><code>mount()</code> is the vue component life cycle hook. During that point, we will set our component status to initial state.</li>
</ol>
<h2 id="file-upload-service">
    <a href="#toc-file-upload-service" target="_blank">
      #
      File Upload Service
    </a> 
  </h2>
<p>Let's proceed to create our service. We will be using <a href="https://github.com/mzabriskie/axios" target="_blank">axios</a> to make HTTP calls.</p>
<h4>Install axios</h4>
<pre><code># install axios
npm install axios --save</code></pre>
<h4>Service</h4>
<pre><code>// file-upload.service.js

import * as axios from 'axios';

const BASE_URL = 'http://localhost:3001';

function upload(formData) {
    const url = `${BASE_URL}/photos/upload`;
    return axios.post(url, formData)
        // get data
        .then(x =&gt; x.data)
        // add url field
        .then(x =&gt; x.map(img =&gt; Object.assign({},
            img, { url: `${BASE_URL}/images/${img.id}` })));
}

export { upload }</code></pre>
<p>Nothing much, the code is pretty expressive itself. We upload the files, wait for the result, map it accordingly.</p>
<p>You may run the application now with <code>npm run dev</code> command. Try uploading a couple of images, and it's working! (Remember to start your backend server)</p>
<h2 id="display-success-and-failed-result">
    <a href="#toc-display-success-and-failed-result" target="_blank">
      #
      Display Success and Failed Result
    </a> 
  </h2>
<p>We can upload the files successfully now. However, there's no indication in UI. Let's update our HTML template.</p>
<pre><code>&lt;!-- App.vue --&gt;

&lt;!-- HTML Template --&gt;
&lt;template&gt;
  &lt;div id="app"&gt;
    &lt;div class="container"&gt;
      ...form...

      &lt;!--SUCCESS--&gt;
      &lt;div v-if="isSuccess"&gt;
        &lt;h2&gt;Uploaded {{ uploadedFiles.length }} file(s) successfully.&lt;/h2&gt;
        &lt;p&gt;
          &lt;a href="javascript:void(0)" @click="reset()"&gt;Upload again&lt;/a&gt;
        &lt;/p&gt;
        &lt;ul class="list-unstyled"&gt;
          &lt;li v-for="item in uploadedFiles"&gt;
            &lt;img :src="item.url" class="img-responsive img-thumbnail" :alt="item.originalName"&gt;
          &lt;/li&gt;
        &lt;/ul&gt;
      &lt;/div&gt;
      &lt;!--FAILED--&gt;
      &lt;div v-if="isFailed"&gt;
        &lt;h2&gt;Uploaded failed.&lt;/h2&gt;
        &lt;p&gt;
          &lt;a href="javascript:void(0)" @click="reset()"&gt;Try again&lt;/a&gt;
        &lt;/p&gt;
        &lt;pre&gt;{{ uploadError }}&lt;/pre&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/template&gt;</code></pre>
<p>Notes:-</p>
<ol>
<li>Display the uploaded image when upload successfully.</li>
<li>Display the error message when upload failed.</li>
</ol>
<h2 id="fake-the-upload-in-front-end">
    <a href="#toc-fake-the-upload-in-front-end" target="_blank">
      #
      Fake the Upload in Front-end
    </a> 
  </h2>
<p>If you are lazy to start the back-end application (Hapi, Express, etc) to handle file upload. Here is a fake service to replace the file upload service.</p>
<pre><code>// file-upload.fake.service.js

function upload(formData) {
    const photos = formData.getAll('photos');
    const promises = photos.map((x) =&gt; getImage(x)
        .then(img =&gt; ({
            id: img,
            originalName: x.name,
            fileName: x.name,
            url: img
        })));
    return Promise.all(promises);
}

function getImage(file) {
    return new Promise((resolve, reject) =&gt; {
        const fReader = new FileReader();
        const img = document.createElement('img');

        fReader.onload = () =&gt; {
            img.src = fReader.result;
            resolve(getBase64Image(img));
        }

        fReader.readAsDataURL(file);
    })
}

function getBase64Image(img) {
    const canvas = document.createElement('canvas');
    canvas.width = img.width;
    canvas.height = img.height;

    const ctx = canvas.getContext('2d');
    ctx.drawImage(img, 0, 0);

    const dataURL = canvas.toDataURL('image/png');

    return dataURL;
}

export { upload }</code></pre>
<p>Came across this solution in this <a href="https://stackoverflow.com/questions/19183180/how-to-save-an-image-to-localstorage-and-display-it-on-the-next-page" target="_blank">Stackoverflow post</a>. Pretty useful. My online <a href="https://vue-file-upload-1126b.firebaseapp.com" target="_blank">demo</a> is using this service. </p>
<p>Basically, what the code do is read the source, draw it in canvas, and save it as data url with the canvas <code>toDataURL</code> function. Learn more about canvas <a href="https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toDataURL" target="_blank">here</a>.</p>
<p>Now you can swap the real service with the fake one.</p>
<pre><code>&lt;!-- App.vue --&gt;
...

&lt;!-- Javascript --&gt;
&lt;script&gt;
  // swap as you need
  import { upload } from './file-upload.fake.service'; // fake service
  // import { upload } from './file-upload.service';   // real service
&lt;/script&gt;

...
</code></pre>
<p>Done! Stop your backend API, refresh your browser, you should see our app is still working, calling fake service instead. </p>
<h2 id="bonus-delay-your-promises">
    <a href="#toc-bonus-delay-your-promises" target="_blank">
      #
      Bonus: Delay Your Promises
    </a> 
  </h2>
<p>Sometimes, you may want to delay the promises to see the state changes. In our case, the file upload may complete too fast. Let's write a helper function for that.</p>
<pre><code>// utils.js

// utils to delay promise
function wait(ms) {
    return (x) =&gt; {
        return new Promise(resolve =&gt; setTimeout(() =&gt; resolve(x), ms));
    };
}

export { wait }
</code></pre>
<p>Then, you can use it in your component</p>
<pre><code>&lt;!-- App.vue --&gt;
...

&lt;!-- Javascript --&gt;
&lt;script&gt;
  import { wait } from './utils';
  ...

  save(formData) {
     ....

        upload(formData)
          .then(wait(1500)) // DEV ONLY: wait for 1.5s 
          .then(x =&gt; {
            this.uploadedFiles = [].concat(x);
            this.currentStatus = STATUS_SUCCESS;
          })
         ...

      },
&lt;/script&gt;</code></pre>
<h2 id="summary">
    <a href="#toc-summary" target="_blank">
      #
      Summary
    </a> 
  </h2>
<p>That's it. This is how you can handle file upload without using any 3rd party libraries and plugins in Vue. It isn't that hard right?</p>
<p>Happy coding!</p>
<p><strong>The UI (Front-end)</strong></p>

<p><strong>The API (Back-end) Tutorials and Sourcode</strong></p>

