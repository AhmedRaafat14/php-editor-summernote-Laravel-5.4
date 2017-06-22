# Summernote integrate with Laravel 5.4

* First of all create in your public folder folder called ['uploads'].
* In ['uploads'] folder create two folders on called ['img'] and other one called ['img-uploads'].
	Other solution just get ['uploads'] folder and put it in your public folder.

***


* In your public folder put the ['summernote'] editor folder in it or any folder in it to use it its up to you ;)

* In your ['routes/web.php'] put your route [' Route::post('/upload_image', '\YourController@uploadImage'); ']

***

>	 Add this function to your controller:
```php	
	    public function uploadImage(Request $request)
	    {
		// A list of permitted file extensions
		if(empty($_FILES['file']))
		{
		    exit(); 
		}
		$errorImgFile = public_path()."/uploads/img/img_upload_error.jpg";
		$destinationFilePath = public_path().'/uploads/img-uploads/'.$_FILES['file']['name'];
		if(!move_uploaded_file($_FILES['file']['tmp_name'], $destinationFilePath)){
		    echo $errorImgFile;
		}
		else{
		    echo url('/').'/public/uploads/img-uploads/'.$_FILES['file']['name'];
		}
	    }
```
***

> In page you should reference to this files in its sections:

	* Header: [fonts, summernote.css]:
	
	  
		<link href="{{ asset('public/summernote/css/font-awesome.css')}}" rel="stylesheet"> -->
          	<link href="{{ asset('public/summernote/css/summernote.css')}}" rel="stylesheet" type="text/css" />
	  
	
	* Footer [js files]:
	  
	
	  	 <script src="{{ asset('public/summernote/js/summernote.js')}}"></script>
	  	 <script src="{{ asset('public/summernote/js/bootstrap.min.js')}}"></script>
	  
***


> In your blade add textarea or div as waht you need and then give it ['id="summernote"' or 'class="summernote"']
	* Textarea:
	
	
		{!! Form::textarea('content',null, array('form-control','id'=>'summernote') ) !!}
	
	* Div:
	
	
		<div id='summernote'></div>
	

* In your page add some input hidden to hold your route url: 
	
	
		{!! Form::hidden('url',url('upload_image'), array('class'=>'url') ) !!}
	

***


* Then at the end of your file in footer add this:
	```javascript
		// If you don't need custom it remove toolbar from under list.
		// Also, you must replac '#' by '.' if you used class instead of id.
		<script>
		    $(document).ready(function() {
			$('#summernote').summernote({
			    height: 200,  
			    toolbar: [
			    ['style', ['bold', 'italic', 'underline', 'clear']],
			    ['font', ['strikethrough', 'superscript', 'subscript']],
			    ['fontsize', ['fontsize']],
			    ['color', ['color']],
			    ['para', ['ul', 'ol', 'paragraph']],
			    ['height', ['height']],
			    ['insert', ['picture']],
			  ]
			});
		    });
		  </script>
	```

* Now you can try and have fun. ^_^ 
* By: [Ahmad Raafat](https://github.com/AhmedRaafat14) and [AymanElshehawy](https://github.com/AymanElshehawy)
