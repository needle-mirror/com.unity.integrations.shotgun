# Advanced Workflows
The tk-config-unity configuration comes with customizations that can greatly
improve artist productivity. 

See [Enabling Advanced Workflows](#enabling-advanced-workflows) for details on how to configure your Shotgun
site to take advantage of these workflows.

## Metadata
When you publish your recordings to Shotgun, Unity embeds the current project path 
and the scene asset path in the created Version entity `sg_unity_metadata` field:

<img src="images/metadata.png" style="border: 1px solid black"/>

This allows Shotgun to start in the right context (right project, 
right scene) when launched from a Version or Note entity.

### Launching from a Version entity
You can launch Unity from a Version entity in the Versions page:

<img src="images/launch_from_version_1.png" style="border: 1px solid black"/>

Or from a Version entity page

<img src="images/launch_from_version_2.png" style="border: 1px solid black"/>

### Launching from a Note entity
You can launch Unity from a Note entity in the Notes page:

<img src="images/launch_from_note_1.png" style="border: 1px solid black"/>

Or from a Note entity page

<img src="images/launch_from_note_2.png" style="border: 1px solid black"/>

In all cases, the Unity Editor should launch directly without going through the 
Unity Hub first.

**Note:** Launching from a Version entity or from a Note entity straight to the 
right Unity project and scene only works if the user has their 
project in the location that is saved in the `sg_unity_metadata` field.
If there is no matching Unity project, then the Unity Hub will
be launched instead.

### Jump to Frame
You can use the Shotgun Panel to automatically select the right Timeline, on the
frame associated with a Shotgun Note. In order to do so:

1. Select `Shotgun Panel...` in the `Shotgun` menu
2. Click on the `Notes` tab and select the Note
3. Click the arrow displayed in the top-right corner of the selected Note
4. Click on `Jump to Frame`

<img src="images/jump_to_frame.png" style="border: 1px solid black"/>

**Note:** The `Jump to Frame` advanced workflow will only work for Note entities
relating to an existing scene in the current Unity project. Also, there must
exist a Main Timeline in the scene.
(see [Establishing the Main Timeline](#establishing-the-main-timeline)).

When successful, the Main Timeline will be selected, and its frame will be set 
to the value reflected by the Shotgun Note entity.

<img src="images/jump_to_frame_focused_main.png" style="border: 1px solid black"/>

#### Establishing the Main Timeline
Timeline Assets can be assigned to multiple Playable Directors in Unity. There 
is no strict concept of a Main Playable Director or Timeline in Unity. The
[Jump to Frame](#jump-to-frame) advanced workflow needs a way to identify the 
Main Timeline so it can select its Playable Director and set its frame value.

`tk-config-unity` determines which Timeline is the Main one by searching for
Game Objects tagged with a specific name. By default, if a Game Object is tagged 
`MainTimeline` and possesses a Playable Director driving a Timeline instance, then
this Timeline instance is considered as the Main Timeline.

To tag a Game Object, select it and choose `MainTimeline` in the list of tags 
<img src="images/tagging_main_timeline.png" style="border: 1px solid black"/>

You can use the `Add Tag...` menu item in the list of tags to add the 
`MainTimeline` tag to the list if it is not present.

The tag name can be configured in the Shotgun Panel settings, for the current
environment. `tk-config-unity` sets this value in 
`env/includes/settings/tk-multi-shotgunpanel.yml`: 

<img src="images/main_timeline_setting.png" style="border: 1px solid black"/>

## Enabling Advanced Workflows
Unity uses a custom Version entity field named `sg_unity_metadata` in order to
save metadata that is used in advanced workflows. Your Shotgun site administrator
needs to add this custom field:

1. As an administrator, go to the Versions page
2. Select `Manage Version Fields...`  

    <img src="images/manage_version_fields.png" style="border: 1px solid black"/>

3. Create a `text` field, named `Unity Metadata`  

    <img src="images/new_field.png" style="border: 1px solid black"/>

    You should see the new field  

    <img src="images/new_field_2.png" style="border: 1px solid black"/>

4. Go into the Fields page  

    <img src="images/fields.png" style="border: 1px solid black"/>  

    There should be a new field on Version entities. The field name should be 
    `Unity Metadata`, the field code should be `sg_unity_metadata`, the data
    type should be `text`  

    <img src="images/validate_field.png" style="border: 1px solid black"/>