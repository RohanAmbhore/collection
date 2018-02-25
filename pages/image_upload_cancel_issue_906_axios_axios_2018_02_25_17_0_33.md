<a href="https://github.com/axios/axios/issues/906">https://github.com/axios/axios/issues/906</a><div id="articleHeader"><h1>              Image upload cancel            #906    </h1></div>


  <div>
    <div>
        <div>
          
          Closed
        </div>
    
    <div>
        <a href="/vedran-milic" target="_blank">vedran-milic</a>  opened this Issue
        <relative-time>on May 20, 2017</relative-time>
        · 2 comments
    </div>
  



    <h2>Comments</h2>
    
      

      

        

          
            





            
  

    



    
      

  
    
      
          <p>How to cancel image upload with post request in axios. I've tried this "<a href="https://github.com/mzabriskie/axios#cancellation" target="_blank">https://github.com/mzabriskie/axios#cancellation</a>" method. But It's not working.</p>
<div><pre>    let CancelToken = axios.CancelToken;
    let source = CancelToken.source();
    let formData = new FormData();
    let current = this;
    let cancelToken = source.token;
    config = {
      onUploadProgress: function(progressEvent) {
        let percentCompleted = Math.round( (progressEvent.loaded * 100) / progressEvent.total );
        current.setState({
          progress: percentCompleted,
          processing: true
        });
        if(percentCompleted === 100) {
          current.setState({
            uploadFinished: true,
            files: []
          });
        }
      }
    };

    axios.post(url, formData, config, cancelToken)
      .then(function (res) {
        if(res.data.Successful) {
          current.setState({
            successMessage:  res.data.Successful,
          });
        }
        console.log('response', res.data.Successful);
        if(res.data.Error) {
          current.setState({
            errorMessage: res.data.Error,
          });
        }
      })
      .catch(function(thrown) {
        if (axios.isCancel(thrown)) {
          console.log('Request canceled', thrown.message);
        } else {
          // handle error
        }
      });</pre></div>
      