---
layout: post
title: What is Silverlight?
---

![Microsoft silverlight](http://d2rormqr1qwzpz.cloudfront.net/uploads/0/5/31462-silverlight_teaser.jpg)

[courtesy](http://www.tested.com/tech/web/3143-rumor-silverlight-5-to-be-the-final-version-of-microsofts-plug-in/)

Recently, I was learning about `Silverlight` for a project. Here is what I'm keeping for future reference:

# Silverlight 5
A Microsoft platform for developing and deploying Rich internet applications. Right now, it's a **depreceated** technology.
Runs as a browser plugin.
Supports .NET languages like `C#` and `VB.NET`, `IronPython` and `IronRuby` using DLR (Dynamic Language Runtime).

# Installation:

There're 3 options:

 - Install silverlight using WPI
 - Install Expression blend for designing purposes
 - Install XNA Game studio for working with 3D

We also need to install the Silverlight SDK.

# Creating a Silverlight project

 - Create a new project in [VS](https://www.visualstudio.com) under `C#` -> `Silverlight`
 
![Creating a Silverlight project](https://lh3.googleusercontent.com/V06tfnM0rmM84LVLfZhIT263P6BcB85WE6Dvf-6JeLN2o90YgYVJgydYh8DtEA5Lg5mmW34TN9JwqRwwlSzvjGSNN2jiMLRXWN_81hw00JAiK50Z2ozgMQSVMud-D1TPnZ_-EoT5MpdI0R2TLpimDDjQHGkX_FhMJHAblBafUozDiv5OtzN9Jk7wSl6uAjla7RQXQvu92YmMVR6SAvmqa2wUl-CYzwFjCPSqXZuSKxsIsttSGN7_Esjd4MtIeSZnXaAjgNYpbEF0jUmU2vO01GnR38lDU85ft7MgIh7pQeRXN1xzJiSDnjREaDn5R5w2HPQJNrk0J15KAu_v0cQvtvaMnDbYznnUEqcCbgkdK0lTEgpY8s_8e9KsFr8i57De_WATOCV0rcLlLz27GuQzcsY3aer-lCUGdeRlU5Cw2y1Rp2Ba_XJy1CW4VXCKJe_aOMuQq01E6iDep74NqRCUXcH-587DCjCoKNkqBQrl9koxxakNDS8hFs_TOByVJQKcJzxCzOiJ0TZ0hdt15M335dqXFtX__QmgmYOWc7onrsFqTvk0PI4DeSTenjtXt8ptQ8S52bOPiHbnJQ332IPm24zBkCAL9Zk=w955-h582-no)

 - Make sure to check **Host the Silverlight application in a new website**

# Running the project

If the developer runtime for `Silverlight` is not installed, the following popup will be shown

![developer runtime for Silverlight is not installed](https://lh3.googleusercontent.com/RdPeAPujcDG9EpUDIcLGI6R0aNr4gCKmgvu6Zz0cTGc6F8J5htppsiNEgLk2VrVWMoGM0gwQxIsUOiSDmoQVbr_vyAnvyqO_yJiSqpLj7L9KGWMtrCj4KAKf6SjR6o3zjPxNzQrmKjYf2RvsCgPRGPjtoTso6ulSwdarqBzTUFmVSgMO6gQdnI-tm2mCshMyF2fgCw1vILn7oKlAFOII5f4SMcnA71JT7-6jsZ3U4C4lpF3AUyF5SHknlKzF80YTy0C9eWl7SjmL1rI9MmpoZ2L4ulkkeRTZkyRnnCUR7WWxQY9D6HPJQ3OVuRdFQ7dwxXm_psvtWhvohTOQndIp-K6N2-vhpGBPNoBDJH1WDAzFyTgs5RB0U8BtDwfNL3lgnkh1hwPUC4TBm01s6wc0vby7JTP78NRpeBA9CSc0IXPs0GxGTsURejRGbN9m4rs9ZeH9XiRe-l6_F4IPxRScyQSobpTYK5pEvU5WUxLz3JGKsYGCqYyO9u2deoBHgfOXdYChet_Jz-eM8gAPUtPHmSTHI7AaN29maOQPLcfMKooYsXjlHshYu-Ri6d5NvBuuxfs5z2hs3lPhNzOkl1Y7Z9qL8acnhIk=w497-h199-no)

When running the project, in case the `Silverlight` is not installed in the browser, the following browser notification will be shown:

![Running Silverlight in Chrome](https://lh3.googleusercontent.com/FNzB1QBestDTfS1pRNWXFd_VAfBAKY4AnQU_D8f7B_3m5so3M-ZVGLPhxaIGJ-d5ep7pMU99zioVkOeUWbxdIP4Eo1EE8d1xBDegZ8ee1X3K-VtukN1H47gdc2mqP8codvc9Ux2NMydnmUw35flAVm4gjqxl77HSDChLC1i-Lcx8N60RzGZi_AwmBecs9-2XjVHoeiR5b0FJ1yRUYs37m96thWmHGW3hNGOrze33BDJqeVs1_fdklnG_Xoa6k9A1BTLykuxIvGkJsNFyt3sTs3QiCpR0pdFU1GqrfPjRvoQLZZ92c13iUT-9J-s6_3r9gVnj8Il0rHZ73pbQmn32JOt8vMOHvfAI8NK34tZALKlRMQV3Jw6dIhtLcw0uN0YJLEpBFlEz9NK85DkUaRra4qOk8a30kpDVc2CUyD8LwMEgbEwJW2ETwxLG04Yyporj4xR1CCqGcWk0-UtS6un9AfS3tEnVJrCeciWmdMFL69orcEYx4JhkDagvz92BuxzgAYJvfXLjtWt1ZQGWbOjIiGXSJu2A9uXAH1qhr0-uL_73S3TN4zmK7-2Az-l_mrB7Dii8sHhItGKWrK7IFPfpGLMUnd7CsWM=w357-h278-no)

>Clicking the install link will take us to the Microsoft website for downloading and installing the plugin

# Visual studio settings

From the VS main menu's Tools -> Options 
 
 - For All languages: enable `word warp` and `line number` under General node
 - Set `Tab` and `indent size` to 2 under Tabs node. Also keep tabs

# Assemblies

There are two types of Microsoft Silverlight assemblies:

The core Silverlight assemblies

 - `mscorlib.dll`
 - `System.Core.dll`
 - `system.dll`
 - `System.Net.dll`
 - `System.Windows.dll`

SDK assemblies, which are used for additional functionalities.

# Structure of a Silverlight project

 - App.xaml file contains Global settings and global events
 - MainPage.xaml is the main Silverlight UI

`Path in web` setting specifies where to put the output `.xap` files. In the image shown, it's `ClientBin` folder.

The initial / startup control can be set from `App.xaml.cs`.

The Silverlight application is compiled into a `.dll` which is then used by the Silverlight runtime.

The `.csproj` file contains the build instructions. During build, VS executes the build instructions contained in the `.csproj` file. One of the instructions calls the language compiler such as `csc.exe` for `C#`, `vbc.exe` for `VB.NET`

Although the process is build, a lot of devs call it compiling.

With Solution configuration set to `Debug`, the Visual studio will create a `Debug` folder inside the `Bin` folder of the project. In general cases, there will be **5** files

 - The application `AppManifest` file - contains the application information
 - The application `.dll` file - the actual code which will be loaded by the Silverlight runtime when executing the project
 - The application `.pdb` file - the portable debug file for the project
 - The application `.xap` file - the zipped bundle of `AppManifest` and the application `.dll`s. This is useful in cases when the application uses SDK assemblies. The zip bundle will help the client download the SDK `.dll`s
 - The application test `.html` file - the application test file generated by the `Properties` -> `Debug` -> `Start Action` set to `Dynamically generate a test page`

# Deployment

When doing the deployment, the mime types need to be mapped in IIS by following the below steps:

 - Select the application in concern from Sites node
 - Double click `Mime Types` and the entries as shown below:

`.xap` -> `application/x-silverlight` - For Silverlight 1 and later
`.xap` -> `application/x-silverlight-2` (-2 means the second implementation of the mime type) - For Silverlight 2 to 5
`.xaml` -> 'application/xaml+xml'

When the application starts up, the `Test` HTML page (generated inside the `Bin` folder) asks the browser to load the Silverlight plugin which is specified in the following tag:

<pre>
<code>
&lt;object data="data:application/x-silverlight-2," type="application/x-silverlight-2" width="100%" height="100%"&gt;
</code>
</pre>

The browser plugin then later asks for the `.xap` file. Which is basically a `.zip` folder containing application and other `.dlls` with information inside the application manifest file.

To not allow browser to load the default error page when the Silverlight plugin isn't available, set the `object` tag's `autoUpgrade` parameter to `false`

<pre><code>
&lt;param name="autoUpgrade" value="false" /&gt;
</code></pre>

with url set to the download link of the required Silverlight plugin. The javascript `onSilverlightError` needs to be used. The `ErrorCode` to watch for is `8001`:

<pre><code>
function onSilverlightError(sender, args) {

	if (args.ErrorCode == 8001) {
		//code to run when correct Silverlight plugin version isn't available
	}
}
</code></pre>

The Silverlight code behind files are in `partial` classes (one holding the event handling, another for the UI handling).
Using a `XAML` element is equal to instantiating a `.NET` class. The `XML` elements are validated against xml namespaces.

# Binding

To assign run time calculation of value and assing to a property we need to use Markup extensions. These classes do binding and resource lookup.

When we assign a property in XAML, we're passing a 

 - string
 - passed through a TypeConverter (and the conversion happens at the compile time)

**Passing values at compile time**

<pre><code>
&lt;TextBox Text='abc' Background='Orange' /&gt;
</code></pre>

**Passing values at run time**

<pre><code>
&lt;TextBox Text='{local:LatinWords}' Background='{StaticResource warning}' /&gt;
</code></pre>

Types of data binding in XAML are:

 - Binding: binding by Data source
 - Template: get value from control template and assign it to property
 - StaticResource: Lookup resource defined in ResourceDictionary
 - Null: Assing null value to preperty
 - Element to element binding:

<pre><code>
&lt;!-- Make this element idenfiable by name --&gt;
&lt;TextBox Text='Hello' x:Name='textHello' Background='Goldenrod' /&gt;
&lt;!-- Assign value from the above textHello to this element --&gt;
&lt;TextBox Text='Goodbye' Background='{Binding ElementName=textHello, Path=Background}' /&gt;
</code></pre>

 - Self binding:

<pre><code>
&lt;!-- Read value red from Text property and assign it to Background property --&gt;
&lt;TextBox Text='Red' Background='{Binding Text, RelativeSource={RelativeSource Self }}' /&gt;
</code></pre>

 - StaticResource binding:

<pre><code>
&lt;!-- Define a static resource --&gt;
&lt;LinearGradientBrush x:Key='seaBrush'&gt;
	&lt;LinearGradientBrush.GradientStops&gt;
		&lt;GradientStop Offset="0" Color="Yellow" /&gt;
		&lt;GradientStop Offset="0.5" Color="Orange" /&gt;
		&lt;GradientStop Offset="0.8" Color="LightCoral" /&gt;
	&lt;/LinearGradientBrush.GradientStops&gt;
&lt;/LinearGradientBrush&gt;

&lt;!-- use the seaBrush static resource for the Background property --&gt;
&lt;TextBox Text='StaticResource' Background='{StaticResource seaBrush}' /&gt;
</code></pre>

 - Null binding:

<pre><code>
&lt;!-- Null MarkupExtension --&gt;
&lt;TextBox Text='Null MarkupExtension' Background='{x:Null}' /&gt;
</code></pre>

 - Custom markup extension binding:

<pre><code>
&lt;!-- The XML namespace abc is defined which refers to abcLib in UserControl --&gt;
&lt;UserControl xmlns:abc='clr-namespace:abcLib;assembly=abcLib' &gt;

		... rest of the code ...

&lt;!-- use our custom markup extension--&gt;
&lt;TextBox Text='{abc:LatinWords WordCount=5}' Background='{x:Null}' /&gt;
&lt;/UserControl&gt;
</code></pre>

and the implementation of custom markup extension is:
 
<pre><code>
namespace abcLib
{
  public class LatinWords : IMarkupExtension&lt;string&gt;
  {

    public bool RandomStartPoint { get; set; }
    public int WordCount { get; set; }


    private Int32 _numberOfWords;
    private static Random ran = new Random();
    private string[] _words;

    public void SetupWords()
    {
      // for demo limit the number of words to 100
      if (WordCount <= 1)
      {
        _numberOfWords = 1;
      }
      if (_numberOfWords > 100)
      {
        _numberOfWords = 100;
      }
      else
      {
        _numberOfWords = WordCount;
      }

      _words = _sourceString.Split(' ');

    }
    public string ProvideValue(IServiceProvider serviceProvider)
    {
      SetupWords();
      int skipCount = 0;
      if (this.RandomStartPoint)
      {
        skipCount = ran.Next(3, 20);
      }
      return string.Join(" ", _words.Skip(skipCount).Take(_numberOfWords).ToArray());
    }

    private string _sourceString = "Lorem ipsum. ";

  }
}</code></pre>
	
# Dependency property system - DPS

Silverlight uses a unique property system which was invented by WPF team. This provides services for UI like Animation, Templates, Styles and reduces critical resource usage (e.g. memory). It has two parts:

 - Dependency properties
 - Attached properties

When creating own user controls, dependency property (e.g. on Button element: FontSize) and .NET property **both** are correct ways to expose a property on them.

 - First, create a dependency property to work with the Silverlight services like data binding
 - Second, create a .NET property to set and read property values in code

**Value resolution priorities**

 1. Active animation
 2. Local value
 3. Templated properties
 4. Style setters
 5. Property value inheritance
 6. Default

Case:
 - If the `local value` for a property is set to **20** and the control in concern is getting animated changing property value from **40 to 80**
 - When we query the value of the property, the value set by the current animation step will be returned, as per the above priority list

**Setting dependency properties using code:**

 - In `XAML` file

<pre><code>
&lt;Button x:Name='sampleButton' Content='Set the Properties in Code' Click='sampleButton_Click' /&gt;
</code></pre>

 - In code behind

<pre><code>
		private void sampleButton_Click(object sender, RoutedEventArgs e)
		{
			sampleButton.FontSize = 40;  // using a .NET wrapper to set value

			double size = sampleButton.FontSize; // use the .NET wrapper to read value

			// use the DP system directly

			sampleButton.SetValue(FontSizeProperty, 30);
			size = (double)sampleButton.GetValue(FontSizeProperty);

		}</code></pre>

Silverlight elements and controls (default or custom) have lots of dependency properties. This system provides services such as animation, data binding, control templates and styles to the Silverlight elements.To get these services a developer needs to write 'ugly' registration code.

An example of declaring and registering a dependency property is:

<pre><code>
	public partial class StarShape : UserControl {

	public StarShape()
	{
		InitializeComponent();
	}

	//declaring
	public static readonly DependencyProperty PointsProperty;

		//registering
		static StarShape()
		{

			// 2. Register with the DP system
			PointsProperty = DependencyProperty.Register("Points", typeof(double), typeof(StarShape), null);

		}
	}</code></pre>

Notice that the property is declared readonly, which means it can only be instantiated in it's static constructor.

# Attached dependency property

They are a special dependency property to provide decoupled extensible model. We can think of it as a 'global property' meaning it is available to all controls in Silverlight runtime.

It is owned and registered by a Type. The method for the same is `DependencyProperty.RegisterAttached`. It uses the dotted syntax `TypeName.AttachedProperty`. These properties are mostly used in layout panels Canvas, Grid, DockPanel.

**Key points:**

 - Attached property value is stored in DPS
 - Value is assigned with element assigning the value
 - The owning class will query the value from the DPs

[Photos](https://goo.gl/photos/fWU5PoCK333JNVpA8)