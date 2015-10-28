jQuery.filer 1.0.3
============
jQuery.filer - Simple HTML5 File Uploader, a plugin tool for jQuery which change completely File Input and make it with multiple file selection, drag&drop support, different validations, thumbnails, icons, instant upload, print-screen upload and many other features and options.

<b><a href="http://filer.grandesign.md/" target="blank">Demo</a></b> | <b><a href="http://filer.grandesign.md/#documentation" target="blank">Documentation</a></b> | <b><a href="http://filer.grandesign.md/#support" target="blank">Support & Donate</a></b>


![Cover](http://filer.grandesign.md/images/content/cover.jpg "jQuery.filer")

Features
-------
* Completely change File Input
* Upload files after choosing
* Add more files to input without uploading them
* Validate files(limit, size, extension)
* Create thumbs
* Custom icons for each type of file
* Custom templates & themes for: input, thumbs, icons
* Remove Choosed/Uploaded files
* Append existing files to input for a preview
* Image paste from clipboard
* Custom captions
* Custom callbacks
* Templates inline variables, ex: {{fi-limit}}
* All icons in a one beautiful font
* Drag & Drop Option
* Trigger options

Browser Support
-------
* Chrome 13+
* Firefox 3.6+
* Safari 6+
* Opera 11.1+
* Maxthon 3.4+
* Internet Explorer 10+
* and others that supports HTML5

Server support
-------
* ASP.NET
* ColdFusion
* Node.js
* PHP
* Perl
* Rails
* Python
* and others that supports standart HTML form file uploads

Usage
-------
__Styles:__

Include the jquery.filer css file in your html page.
~~~~ html
<link href="./css/jquery.filer.css" type="text/css" rel="stylesheet" />
<link href="./css/themes/jquery.filer-dragdropbox-theme.css" type="text/css" rel="stylesheet" />
~~~~

__Scripts:__

Include the jQuery library and jquery.filer script file in your html page. 
~~~~ html
<script src="http://code.jquery.com/jquery-latest.min.js"></script>
<script src="./js/jquery.filer.min.js"></script>
~~~~

__HTML:__

Create an input file element.
~~~~ html
<form action="./php/upload.php" method="post" enctype="multipart/form-data">
    <input type="file" name="files[]" id="input_file" multiple="multiple">
    <input type="submit">
</form>
~~~~

__Javascript:__

The plugin is named "filer" and can be applied to any element. You will probably also specify some options while applying the plugin. If you are not familiar with jQuery, please, read this <a href="http://learn.jquery.com/about-jquery/how-jquery-works/" target="_blank">tutorial for beginners</a>.
~~~~ javascript
$(document).ready(function() {
	$('#input_file').filer({
        limit: null,
        maxSize: null,
        extensions: null,
        changeInput: true,
        showThumbs: true,
        appendTo: null,
        theme: "default",
        templates: {
            box: '<ul class="jFiler-item-list"></ul>',
            item: '<li class="jFiler-item">\
                        <div class="jFiler-item-container">\
                            <div class="jFiler-item-inner">\
                                <div class="jFiler-item-thumb">\
                                    <div class="jFiler-item-status"></div>\
                                    <div class="jFiler-item-info">\
                                        <span class="jFiler-item-title"><b title="{{fi-name}}">{{fi-name | limitTo: 25}}</b></span>\
                                    </div>\
                                    {{fi-image}}\
                                </div>\
                                <div class="jFiler-item-assets jFiler-row">\
                                    <ul class="list-inline pull-left">\
                                        <li>{{fi-progressBar}}</li>\
                                    </ul>\
                                    <ul class="list-inline pull-right">\
                                        <li><a class="icon-jfi-trash jFiler-item-trash-action"></a></li>\
                                    </ul>\
                                </div>\
                            </div>\
                        </div>\
                    </li>',
            itemAppend: '<li class="jFiler-item">\
                        <div class="jFiler-item-container">\
                            <div class="jFiler-item-inner">\
                                <div class="jFiler-item-thumb">\
                                    <div class="jFiler-item-status"></div>\
                                    <div class="jFiler-item-info">\
                                        <span class="jFiler-item-title"><b title="{{fi-name}}">{{fi-name | limitTo: 25}}</b></span>\
                                    </div>\
                                    {{fi-image}}\
                                </div>\
                                <div class="jFiler-item-assets jFiler-row">\
                                    <ul class="list-inline pull-left">\
                                        <span class="jFiler-item-others">{{fi-icon}} {{fi-size2}}</span>\
                                    </ul>\
                                    <ul class="list-inline pull-right">\
                                        <li><a class="icon-jfi-trash jFiler-item-trash-action"></a></li>\
                                    </ul>\
                                </div>\
                            </div>\
                        </div>\
                    </li>',
            progressBar: '<div class="bar"></div>',
            itemAppendToEnd: false,
            removeConfirmation: true,
            _selectors: {
                list: '.jFiler-item-list',
                item: '.jFiler-item',
                progressBar: '.bar',
                remove: '.jFiler-item-trash-action',
            }
        },
        uploadFile: {
            url: "./php/upload.php",
            data: {},
            type: 'POST',
            enctype: 'multipart/form-data',
            beforeSend: function(){},
            success: function(data, el){
                var parent = el.find(".jFiler-jProgressBar").parent();
                el.find(".jFiler-jProgressBar").fadeOut("slow", function(){
                    $("<div class=\"jFiler-item-others text-success\"><i class=\"icon-jfi-check-circle\"></i> Success</div>").hide().appendTo(parent).fadeIn("slow");    
                });
            },
            error: function(el){
                var parent = el.find(".jFiler-jProgressBar").parent();
                el.find(".jFiler-jProgressBar").fadeOut("slow", function(){
                    $("<div class=\"jFiler-item-others text-error\"><i class=\"icon-jfi-minus-circle\"></i> Error</div>").hide().appendTo(parent).fadeIn("slow");    
                });
            },
            statusCode: {},
            onProgress: function(){},
            onComplete: function(){}
        },
        dragDrop: {
            dragEnter: null,
            dragLeave: null,
            drop: null,
        },
        addMore: true,
        clipBoardPaste: true,
        excludeName: null,
        files: null,
        beforeShow: function(){return true},
        onSelect: function(){},
        afterShow: function(){},
        onRemove: function(){},
        onEmpty: function(){},
        captions: {
            button: "Choose Files",
            feedback: "Choose files To Upload",
            feedback2: "files were chosen",
            drop: "Drop file here to Upload",
            removeConfirmation: "Are you sure you want to remove this file?",
            errors: {
                filesLimit: "Only {{fi-limit}} files are allowed to be uploaded.",
                filesType: "Only Images are allowed to be uploaded.",
                filesSize: "{{fi-name}} is too large! Please upload file up to {{fi-maxSize}} MB.",
                filesSizeAll: "Files you've choosed are too large! Please upload files up to {{fi-maxSize}} MB."
            }
        }
    });
});
~~~~

Options & Features
-------
Fully documentation of plugin options and features.

__Options:__
* __limit__ Maximum Limit of files. {null, Number}
* __maxSize__ Maximum Size of files. {null, Number(in MB's)}
* __extensions__ Whitelist for file extension. {null, Array}
* __changeInput__ Change input. {Boolean, String(HTML element), Object(DOM Element)}
* __showThumbs__ Show input files as thumbnails. {Boolean}
* __appendTo__ Append thumbnails to element. {null, String(Dom Element)}
* __theme__ jQuery.filer theme. {null, String}
* __templates__
    * __box__ Thumbnails box element {null, String}
    * __item__ Thumbnails file item element {String(use <a href="#filer-variables">Filer Variables</a>), Function}
    * __itemAppend__ Thumbnails appended file item element {String(use <a href="#filer-variables">Filer Variables</a>), Function}
    * __progressBar__ Thumbnails file item upload progress bar element {String}
    * __itemAppendToEnd__ Append file item to the end of list {Boolean}
    * __removeConfirmation__ Remove file confirmation {Boolean}
    * __selectors__
        * __list__ List selector {String}
        * __item__ Item selector {String}
        * __progressBar__ Progress bar selector {String}
        * __remove__ Remove button selector {String}
* __uploadFile__
    * __url__ URL to which the request is sent {String}
    * __data__ Data to be sent to the server {Object}
    * __type__ The type of request {String}
    * __enctype__ Request enctype {String}
    * __beforeSend__ A pre-request callback function {Function}
    * __success__ A function to be called if the request succeeds {Function}
    * __error__ A function to be called if the request fails {Function}
    * __statusCode__ An object of numeric HTTP codes {Object}
    * __onProgress__ A function called while uploading file with progress percentage {Function}
    * __onComplete__ A function called when all files were uploaded {Function}
* __dragDrop__
    * __dragEnter__ A function that is fired when a dragged element enters the input. {Function}
    * __dragLeave__ A function that is fired when a dragged element leaves the input. {Function}
    * __drop__ A function that is fired when a dragged element is dropped on a valid drop target.
* __addMore__ Multiple file selection without instant uploading {Boolean}
* __clipBoardPaste__ Printscreen paste and upload {Boolean}
* __excludeName__ Removed files input name {null, String} Default: jfiler-items-exclude-(input file name)-(input index)
* __files__ Already uploaded files list {null, Array} Ex: [{"name":"appended_file.jpg","size":5453,"type":"image/jpg",file:"/path/to/file/appended_file.jpg"}]
* __beforeShow__ A function that is fired before showing thunbnails {Function}
* __onSelect__ A function that is fired after selecting files {Function}
* __afterShow__ A function that is fired after appending all thumbnails items {Function}
* __onRemove__ A function that is fired after deleting a file {Function}
* __onEmpty__ A function that is fired when no files are selected {Function}
* __captions__
    * __button__ New Input button text {String}
    * __feedback__ New Input field text {String}
    * __feedback2__ New Input after choosing files text {String}
    * __drop__ New Input on drag text {String}
    * __removeConfirmation__ Remove file confirmation text {String}
    * __errors__
        * __filesLimit__ {String(use <a href="#filer-variables">Filer Variables</a>)}
        * __filesType__ {String(use <a href="#filer-variables">Filer Variables</a>)}
        * __filesSize__ {String(use <a href="#filer-variables">Filer Variables</a>)}
        * __filesSizeAll__ {String(use <a href="#filer-variables">Filer Variables</a>)}

__Triggers:__
* $('#input_file').trigger("filer.append", {files:[]})
* $('#input_file').trigger("filer.remove", {id:0})
* $('#input_file').trigger("filer.reset")
* $('#input_file').trigger("filer.getList", {files:[]})
* $('#input_file').trigger("filer.retry", here_is_file_id)

__Attributes:__
* data-jfiler-name | name of input (is used while applying plugin to a non file input)
* data-jfiler-limit | files limit
* data-jfiler-maxSize | files maximum size
* data-jfiler-extensions | separeted with comma
* data-jfiler-changeInput | {Boolean, String}
* data-jfiler-showThumbs | show thumbnails
* data-jfiler-appendTo | append thumbnails to selector
* data-jfiler-theme | custom filer theme
* data-jfiler-excludeName | exclude files input name
* data-jfiler-files | append files, ex: "{"files":[{"name":"appended_file.jpg","size":5453,"type":"image/jpg",file:"/path/to/file/appended_file.jpg"}]}"

Filer Variables
-------
Filer Variables are very simple to use in filer string options. To use them just write <b>{{fi-(variable name)}}</b>. Below are all available combinations that can be used:
* fi-name
* fi-size
* fi-size2
* fi-type
* fi-extension
* fi-icon
* fi-icon2
* fi-id
* fi-image
* fi-progressBar
* fi-limit
* fi-maxSize

Contribute
-------
Want to be part of this project? Great! All are welcome!
Whether you have a great feature request or you fancy owning a task from the road map above feel free to get in touch.
<br>
By <b>themes</b> you can contribute to plugin by making a <a href="https://github.com/CreativeDream/jquery.filer/pulls" target="_blank">Pull Request</a> to <i>/css/themes/</i> and writing a short description containing plugin templates options.

Support
-------
Questions or need help? You can ask it using <a href="http://stackoverflow.com/questions/ask?tags=jQuery,jquery.filer" target="_blank">StackOverflow</a> site where you are most likely to get answer quickly. Make sure you add the tags "jquery" and "jquery.filer" when posting.

If you run into an issue and need to report a bug or you just have a question, please create an <a href="https://github.com/CreativeDream/jquery.filer/issues" target="_blank">Issue</a> on GitHub issues and we will investigate it.

<b>Make a donation</b> - jQuery.filer is free and open source and your donations will help us to develop it. You can support our project by donating with PayPal. All contributions, small or great, are very much appreciated. Thanks!
<br><br>
<a href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=WFVGJ66RW22GJ" target="_blank"><img src="http://grandesign.md/__cr/1445905675_paypal-curved.png"></a>

PHP File Uploader
-------
PHP File Uploader is an easy to use, hi-performance File Upload Script which allows you to upload files to webserver. You can get it on the link below.
<br><b><a href="https://github.com/CreativeDream/php-uploader" target="blank">PHP Uploader</a></b>

License
-------
> Licensed under <a href="http://opensource.org/licenses/MIT">MIT license</a>.
