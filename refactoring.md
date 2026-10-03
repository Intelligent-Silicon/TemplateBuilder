# Refactoring

The AppGen already handles alot of the refactoring tasks that other more popular development tools sometimes struggle with resulting in the need to file bug reports.

TemplateBuilder has taken refactoring to another level, with the introduction of Ambifixes. 


### Ambifixes

Ambifixes are (unique) alphanumeric strings that can be prefixed or suffixed to a procedure name, template name, template description or template group to ensure the correct version is used in a template, or program DLL.

Three types of Ambifixes currently exist, the rules are shown below, which apply globally for each ```.App``` file, with an optional procedure level override for procedure level customisation.

| Ambifix Type | Syntax | RegEx | Notes |
| -- | -- | -- | -- |
| Template Name | Clarion Label | ```^[a-zA-Z_][a-zA-Z0-9_:\.]+$```] | https://clarion.help/doku.php?id=declaration_and_statement_labels.htm also used for AppGen procedure names. |
| Template Description | String constant | ```^'.?'$``` | https://clarion.help/doku.php?id=string_constants.htm |
| Group Symbol | Clarion Symbol | ```^%[a-zA-Z0-9]+$``` | |

![Ambifix Global ](https://github.com/Intelligent-Silicon/TemplateBuilder/blob/main/pics/ambifixglobal.jpg)

Whilst it can now remove the [DLL Hell](https://en.wikipedia.org/wiki/DLL_hell) aspect from your own program DLL's, it doesnt completely remove DLL Hell when using external libraries and it doesnt remove a hacker's ability to use [Shim's](https://cloud.google.com/blog/topics/threat-intelligence/abusing-dll-misconfigurations/) to intercept the data your program is exchanging with DLL's, it just introduces a new hurdle.

If using Ambifixes with a new unique GUID for every version released to a customer, the GUID can help identify which customer has lax computer security if a program should ever turn up on a piracy warez site.

And if using a new unique GUID for every workstation a program is to be installed on, this will increase the workload for IT administrators having to create a file signature hash for [MS Windows Group Policy](https://learn.microsoft.com/en-us/windows-server/identity/software-restriction-policies/work-with-software-restriction-policies-rules) or [MS AppLocker](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/app-control-for-business/applocker/create-a-rule-that-uses-a-file-hash-condition).

A unique Ambifix can be used for every instance of a program that is generated and compiled, or for every instance of a template that is built by TemplateBuilder.

You have full control over the Ambifix, you can choose to make it a GUID, a version number, or just a simple alphanumeric string like the type seen appended to the end of Microsoft Store App, provided its compliant with the rules for a label, string constant or ```%symbol```.

With Clarion 6's DDE remote control, and Clarion 7+ [Command Line Interface Utility](https://clarion.help/doku.php?id=customizing_the_command_line_interface_clarioncl_exe_.htm&s[]=command&s[]=line), the ability to generate a unique alphanumeric Ambifix, can force more work onto hacker's as the lifespan of their shim's becomes shorter with each new version.

The underlying procedure name remains unchanged in the AppGen, so the different AppGen views retain their familiarity by not changing the procedure names seen in the AppGen, but the generated code, beit Clarion template language code, Clarion language code or any other program language code, is modified automatically at code generation time.


In terms of templates, the Ambifix ensures a template can only load the correct templates and groups, when multiple versions of a template are registered in the Template Registry and avoids loading the wrong templates and groups because a 3rd party template has used the same name for a template or group symbol.

This can be useful for side by side development of new template versions, whilst keeping existing versions registered in the Template Registry, without any conflict.

Once template development is completed, its just as quick switching off Ambifixes and have everything resort back to the original template name or group symbol name, both derived from the procedure name used in the AppGen before shipping the upgraded template to users. This final step also removes the continuity issues where user's have to refill the template prompts again, whilst giving template developers the option to introduce new templates as seen with the Edit-In-Place templates.

The ability to switch off Ambifixes at the global ```.App``` file level and procedure levels, also enables common template code functionality to be used to create template language library's to ensure a high standard of compliance is maintained when filling in template prompts. A shared or common template code library can enforce a template prompt string is capitalised, has no spaces or underscores, complies to naming schemes and more...

![Ambifixes](https://github.com/Intelligent-Silicon/TemplateBuilder/blob/main/pics/ambifixes.jpg)

Class Writer 2 doesnt use Ambifixes, Class Writer 3 and 3.1 do, enabling all three templates to co-exist in the template registry without any interaction between them or any other template.

The prompts stay identical, but as ClassWriter is its own independent template chain, to switch between different versions currently requires an export to a TXA file, the template particulars changed and then the TXA imported into a new app.

If these templates were any other template type that works with a template chain like the ABC, Clarion or CWHandyTools, inside the AppGen its as simple as just uninstalling one version and installing another. 

Its as simple as that because the prompts can remain the same and the AppGen keeps a record of all prompts used even after a template has been removed from an app. 

This way developers can work on their time line, and can choose the 3rd party developers version that bests suits their needs.

However that gets a bit muddy because in practice, currently bug fixes are generally rolled into new versions along with new features because it takes additional resource to maintain multiple branches, although TemplateBuilder now makes this much much easier.



### Breaking up a Template

Just like with Clarion Windows programs, the need to break up large code bases into smaller sections often arises over time. See https://clarion.help/doku.php?id=development_and_deployment_strategies.htm&s[]=sub&s[]=application

TemplateBuilder now lets the developer break up a single ```.App``` AppGen file template into multiple ```.App``` AppGen files.

This helps to maintain code standards, logical grouping of functionality, readability and maintainability, whilst providing the ability to introduce experimental code to a template quickly and easily. 

The developer is also able to introduce their own common template functionality, for enforcing prompt standards and more, across template suites, exceeding the functionality built into the base template language.

![Ambifixes](https://github.com/Intelligent-Silicon/TemplateBuilder/blob/main/pics/externals.jpg)


ClassWriter3 currently sits at over 550 procedures across multiple ```.App``` files, with more functionality being added daily, to ensure new users can get up to speed on their first attempt, without having to consult help documentation!


![Ambifixes](https://github.com/Intelligent-Silicon/TemplateBuilder/blob/main/pics/classwriter3.jpg)

![Ambifixes](https://github.com/Intelligent-Silicon/TemplateBuilder/blob/main/pics/classwriter3.1.jpg)

To create a new version of a template, copy the existing app files into a new folder, update the Ambifixes in each ```.App``` file and generated the template code. Its that simple.