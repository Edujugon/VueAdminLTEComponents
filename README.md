# Vue AdminLTE Components

Set of Vue.js components with adminLTE.

Most of these components have been created for a specific project, that's why they have some custom props names.
You can use these components as template and change any name/prop as per your need.

## Alert Component

Support all types of adminLTE alerts

###Properties:

**type** 

Options: danger, info, warning, success

**icon**

Options: ban, info , warning, check

**title**

If no prop passed by default will be set -> Alert!

**message**


**canBeClosed**

Options: `true/false`

By default is `true`

Example of use: `:can-be-closed=false`

## SocialWidgetStyleOne Component

If no image prop passed, all header data will be displayed centered