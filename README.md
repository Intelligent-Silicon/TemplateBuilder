# TemplateBuilder
Some recovered files for the Template Builder.

Not complete, but files will show how it was constructed.

Files recovered using PhotoRec, OSForensics couldnt recover any files in the end.

Nameing Schema

%TB2valStringEncapsulationRemove

TB = Template Builder
[1-5] = Version

val = Validate Procedure

Rest is the name.

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




