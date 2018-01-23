<a href="https://research.fb.com/facebook-open-sources-detectron/">https://research.fb.com/facebook-open-sources-detectron/</a><div id="articleHeader"><h1>Facebook open sources Detectron</h1></div>				<p><small>By: <a href="https://research.fb.com/people/girshick-ross/" target="_blank">Ross Girshick</a></small></p>
			
		
	</header>

	
				
		
		
			

			
				<p>Today, Facebook AI Research (FAIR) open sourced <a href="https://research.fb.com/downloads/detectron/" target="_blank">Detectron</a> — our state-of-the-art platform for object detection research.</p>
<p>The Detectron project was started in July 2016 with the goal of creating a fast and flexible object detection system built on Caffe2, which was then in early alpha development. Over the last year and a half, the codebase has matured and supported a large number of our projects, including <a href="https://arxiv.org/abs/1703.06870" target="_blank">Mask R-CNN</a> and <a href="https://arxiv.org/abs/1708.02002" target="_blank">Focal Loss for Dense Object Detection</a>, which won the Marr Prize and Best Student Paper awards, respectively, at ICCV 2017. These algorithms, powered by Detectron, provide intuitive models for important computer vision tasks, such as instance segmentation, and have played a key role in the unprecedented advancement of visual perception systems that our community has achieved in recent years.</p>
<p>Beyond research, a number of Facebook teams use this platform to train custom models for a variety of applications including augmented reality and community integrity. Once trained, these models can be deployed in the cloud and on mobile devices, powered by the highly efficient Caffe2 runtime.</p>
<p>Our goal in open sourcing Detectron is to make our research as open as possible and to accelerate research in labs across the world. With its release, the research community will be able to reproduce our results and have access to the same software platform that FAIR uses every day.</p>
<p>Detectron is available under the Apache 2.0 license at <a href="https://github.com/facebookresearch/Detectron" target="_blank">https://github.com/facebookresearch/Detectron</a>. We’re also releasing extensive performance baselines for more than 70 pre-trained models that are available to download from our model zoo.</p>
				
			