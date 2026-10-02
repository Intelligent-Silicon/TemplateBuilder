# Refactoring

The AppGen already handles alot of the refactoring tasks that other more popular development tools sometimes struggle with resulting in the need to file bug reports.

TemplateBuilder has taken refactoring to another level, with the introduction of Ambifixes. 


### Ambifixes

Ambifixes are (unique) alphanumeric strings that can be prefixed or suffixed to a procedure name, template name, template description or template group to ensure the correct version is used in a template, or program DLL.

3 Ambifixes currently exist, one for the Template name, that complies with the rules of defining a Label, one for the description string which has few rules due to it being a string, and one for ```#Group``` names, that complies with rules for using a template ```%symbol```.

Whilst it can now remove the [DLL Hell](https://en.wikipedia.org/wiki/DLL_hell) aspect from your own program DLL's, it doesnt completely remove the hacker's ability to use [Shim's](https://cloud.google.com/blog/topics/threat-intelligence/abusing-dll-misconfigurations/) to intercept the data your program is exchanging with DLL's.

A unique Ambifix can be used for every instance of a program that is generated and compiled, or for every instance of template that is built by TemplateBuilder.

You have full control over the Ambifix, you can choose to make it a GUID, a version number, or just an simple alphanumeric string like the type seen with Microsoft Store Apps, provided its compliant with the rules for a label, string or ```%symbol```.

With Clarion 6's DDE remote control, and Clarion 7+ [Command Line Interface Utility](https://clarion.help/doku.php?id=customizing_the_command_line_interface_clarioncl_exe_.htm&s[]=command&s[]=line), the ability to generate a unique alphanumeric Ambifix, can force more work onto hacker's as the lifespan of their shim's becomes shorter with each new version.

The underlying procedure name remains unchanged in the AppGen, so the different AppGen views retain their familiarity by not changing the procedure names, but the generated code, beit Clarion template language code or Clarion language code, is updated automatically at the time of code generation. 


In terms of templates, the Ambifix ensure's a template can only load the correct templates and groups, when multiple versions of a template are registered in the Template Registry and avoids loading the wrong templates and groups because a 3rd party template developer has used the same name.

This can be useful for development of new template versions, whilst keeping existing versions registered in the Template Registry, without any conflict.

Once template development is completed, its just as quick switching off Ambifixes and have everything resort back to the original procedure name before shipping the upgraded template to users. This removes the continuity issues where user's have to fill in the template prompts again.

![Ambifixes](https://github.com/Intelligent-Silicon/TemplateBuilder/blob/main/Pics/ambifixes.jpg)






