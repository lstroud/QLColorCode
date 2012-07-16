#QLColorCode

Original code at: <https://github.com/n8gray/QLColorCode/>   
This fork at: <https://github.com/lstroud/QLColorCode/>  

This is a Quick Look plugin that renders source code with syntax highlighting,
using the Highlight library: <http://www.andre-simon.de/index.html>

##Building and Installing
First you need to install 'highlight'.  You can use brew for this.  If you don't use brew, you can find more information at: <http://mxcl.github.com/homebrew/>

With brew installed, you would simple run:  
	`brew install highlight`

After that, you will need to build the project in xcode.  It's been updated for the lion frameworks.  So, you shouldn't need to do anything besides Project -> Build.

The xcode build process will install the plugin (one of the build phases). 

If you need to manually install it, copy the 'QLColorCode.qlgenerator' file into the /Library/QuickLook or ~/Library/QuickLook folders.

##Configuration  
If you want to configure QLColorCode, there are several "defaults" commands 
that could be useful:

######Setting the text encoding (default is UTF-8)  
These two settings are required. The first sets Highlight's encoding, the second sets Webkit's:    
`defaults write org.n8gray.QLColorCode textEncoding UTF-16`  
`defaults write org.n8gray.QLColorCode webkitTextEncoding UTF-16`  
    
###### Setting the font  
`defaults write org.n8gray.QLColorCode font Monaco`  
`defaults write org.n8gray.QLColorCode fontSizePoints 9`  
    
######the color style   
See <http://www.andre-simon.de/dokuwiki/doku.php?id=theme_examples> for some examples.  

Highlight comes with a large number of themes.  If you installed highlight using brew, then the themes are in /usr/local/share/highlight/themes.  The filename without the extension is the theme name.  Here is how you change the theme:  

`defaults write org.n8gray.QLColorCode hlTheme edit-xcode`  

I've even added a them of my own.  It a file called lesismore.theme in the project directory.  To use it, you will need to copy it into the highlight themes directory.  

There is also a user.css file in the project directory.  If you move it into your highlight config directory (hlconfpath in colorize.sh), then you can use css to style margin, padding, borders, etc for line numbers.

######other config settings  
You can pass in any of highlight's other configuration parameters ('highlight -h' for a list) using the extraHLFlags setting.  For example, this setting will print line numbers and wrap text that is too wide:          
`defaults write org.n8gray.QLColorCode extraHLFlags '-l -W'`  
      
or, the maximum size (in bytes) for previewed files:  
`defaults write org.n8gray.QLColorCode maxFileSize 1000000`  
   
Here are some useful 'highlight' command-line flags (from the man page):  
```	       
-F, --reformat=<style> reformat output in given style.   <style>=[ansi,  gnu,  kr, java, linux]  
	
-J, --line-length=<num> line length before wrapping (see -W, -V)  
	
-j, --line-number-length=<num> line number length incl. left padding  
	
-l, --linenumbers print line numbers in output file  
	
-t  --replace-tabs=<num> replace tabs by num spaces  
	
-V, --wrap-simple wrap long lines without indenting function  parameters  and statements  
	
-W, --wrap wrap long lines  
	
-z, --zeroes fill leading space of line numbers with zeroes  
	
--kw-case=<upper|lower|capitalize> control case of case insensitive keywords  
```	

If you have installed highlight into an alternate location, your will need to edit the paths in colorize.sh 