# TemplateBuilder
Some recovered files for the Template Builder.

Not complete, but files will show how it was constructed.

Files recovered using PhotoRec, OSForensics couldnt recover any files in the end.

Example Nameing Schema

%TB2valStringEncapsulationRemove

TB = Template Builder
[1-5] = Version number.

val = Validate Procedure

grp = Group Procedure

The rest is the name of the procedure.

Why is this public. This is all I have left to prove what I had been doing for about 5 years. 
Prior to this, I'd probably spent another 5 years experimenting with different apps (exe's) and templates to explore ways to develop an app that could write templates. This was pursued first because of the problem which exists that its currently impossible to secure a template and prevent it from being copied, where as exe's can be secured more easily to prevent them from being copied. 

Why is this important? Here in Exeter if you cant prove what you have been doing using social media, the people of Exeter and quite likely elsewhere in the UK will automatically assume the worst which is you have been in prison for a number of years. Thanks Zuck!

So in order to avoid any further personal trouble and attacks because the state both local and nation will not deviate from its processes, I'm effectively making it known something which will benefit some savvy programmers elsewhere in the world. And the UK wonder's why its going down the pan, when people are forced to give away their competitive advantage and years of work!

At the same time, it pains me to see years of work go to waste, so maybe someone else will see how the templates can be used to build themselves and then expanded with #RunDll especialy in todays world of very long Markov Chains aka Large Language Models (LLM)'s like ChatGPT.

This also means, the template builder could generate code in any language for any platform, because the slow esoteric nature of the template language could be accelerated quickly by virtue of using a template to build further templates, by just filling in some prompt's. Something every Clarion programmer knows and generally loves which is why they still use Clarion.


```
    #Prompt('Name',@s255),%TB2TemplateExtensionName,Req,At(60,,120,10),Default(%TB2grpTemplateExtensionDefaultName(%Procedure))
        #Validate(%TB2valStringEncapsulationRemove(%TB2TemplateExtensionName),'#Validate(%TB2valStringEncapsulationRemove(%TB2TemplateExtensionName))')
        #Validate(%TB2valValidateReservedWord(%TB2TemplateExtensionName),'Reserved Words not allowed')
        #Validate(%TB2valValidateClarionLabel(%TB2TemplateExtensionName),'Invalid Clarion Label')
        #Validate(%TB2valValidateNamingSchemaExtension(%TB2TemplateExtensionName),'Invalid Naming Scheme')
    #Prompt('''Description''',@s255),%TB2TemplateExtensionDescription,Req,At(60,,120,10),Default(%TB2grpTemplateExtensionDefaultDescription())
        #Validate(%TB2valStringEncapsulationRemove(%TB2TemplateExtensionDescription),'#Validate(%TB2valStringEncapsulationRemove(%TB2TemplateExtensionDescription))')
        #Validate(%TB2valValidateStringConstant(%TB2TemplateExtensionDescription),'#Validate(%TB2valValidateStringConstant(%TB2TemplateExtensionDescription))')
        #Validate(%TB2valStringEncapsulationAdd(%TB2TemplateExtensionDescription),'#Validate(%TB2valStringEncapsulationAdd(%TB2TemplateExtensionDescription))')
    #Prompt('''Target''',@s255),%TB2TemplateExtensionTarget,At(60,,120,10),Default(%TB2grpTemplateExtensionDefaultTarget())
        #Validate(%TB2valStringEncapsulationRemove(%TB2TemplateExtensionTarget),'#Validate(%TB2valStringEncapsulationRemove(%TB2TemplateExtensionTarget))')
        #Validate(%TB2valValidateStringConstant(%TB2TemplateExtensionTarget),'#Validate(%TB2valValidateStringConstant(%TB2TemplateExtensionTarget))')
        #Validate(%TB2valStringEncapsulationAdd(%TB2TemplateExtensionTarget),'#Validate(%TB2valStringEncapsulationAdd(%TB2TemplateExtensionTarget))')
    #Prompt('''~helpid''',@s255),%TB2TemplateExtensionHelpID,At(60,,120,10)
        #Validate(%TB2valStringEncapsulationRemove(%TB2TemplateExtensionHelpID),'#Validate(%TB2valStringEncapsulationRemove(%TB2TemplateExtensionHelpID))')
        #Validate(%TB2valValidateHelpID(%TB2TemplateExtensionHelpID),'#Validate(%TB2valValidateHelpID(%TB2TemplateExtensionHelpID))')
        #Validate(%TB2valStringEncapsulationAdd(%TB2TemplateExtensionHelpID),'#Validate(%TB2valStringEncapsulationAdd(%TB2TemplateExtensionHelpID))')
    #Prompt('Multi',Check),%TB2TemplateExtensionMulti,At(60)
    #Prompt('Expression',@s255),%TB2TemplateExtensionExpression,At(60,,120,10)
    #Prompt('Show',Check),%TB2TemplateExtensionShow,At(60)
    #Prompt('''Message''',@s255),%TB2TemplateExtensionPrimaryMessage,At(60,,120,10)
        #Validate(%TB2valStringEncapsulationRemove(%TB2TemplateExtensionPrimaryMessage),'#Validate(%TB2valStringEncapsulationRemove(%TB2TemplateExtensionPrimaryMessage))')
        #Validate(%TB2valValidateStringConstant(%TB2TemplateExtensionPrimaryMessage),'#Validate(%TB2valValidateStringConstant(%TB2TemplateExtensionPrimaryMessage))')
        #Validate(%TB2valStringEncapsulationAdd(%TB2TemplateExtensionPrimaryMessage),'#Validate(%TB2valStringEncapsulationAdd(%TB2TemplateExtensionPrimaryMessage))')
```


You can stack multiple #Validates after a #Prompt, this is one of many undocumented features in the template language, which then enables you to standardised the template prompts validation process, by passing parameters which use the \* prefix. This way you can ensure the data keyed into a prompt is valid, without having to deal with Return Values and the issues that comes with, namely invalid datatypes.



An example of using #RunDll. The DLL's were apps specially designed to take a string of data and parse it accordingingly, before processing it.

See f895759712.txt file.


```
%#Declare(%%pIO)
%#Declare(%%ValReturn)

%#Set(%%pIO,%%TB2GlobalPropTemplateOutputFolder)

%#RunDll('C6FolderExists.dll','C6FOLDEREXISTS@FRsc',%%pIO),Release,Win32      

%#IF(%%pIO <> %%True )

    %#Set(%%pIO,%%TB2GlobalPropTemplateOutputFolder)
    %#RunDll('C6FolderCreate.dll','C6FOLDERCREATE@FRsc',%%pIO),Release,Win32   %#! Cant create a Folder with a back slash, this dll needs updating

    %#IF(%%pIO <> %%True )

        %#Error(%%Procedure & '<32,10>Unable to create Template Output Folder %%TB2GlobalPropTemplateOutputFolder' & %%TB2GlobalPropTemplateOutputFolder )
        %#Abort

    %#EndIF


%#EndIF
```