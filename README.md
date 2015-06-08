# UnityTwine
**Play Twine stories in Unity.**

[Twine](http://twinery.org) is an extremely simple and flexible tool for writing interactive stories. [Unity](http://unity3d.com) is a powerful and feature-rich engine for building games and interactive experiences. [UnityTwine](http://github.com/daterre/UnityTwine) brings the two worlds together.

Writers can independently design and test their stories as they would a normal Twine story;
programmers and artists can develop the interaction and presentation without worrying about flow control. When imported to Unity, UnityTwine kicks in and bridges the gap. 

####Getting started
1. [Download the latest UnityTwine release](https://github.com/daterre/UnityTwine/tree/master/Assets/Plugins/UnityTwine).
2. Export .twee files from Twine 1 or 2 ([instructions](#exporting-twee-files-from-twine)) and drag into Unity
3. Add the generated script to your scene
4. Use [hooks](#hooks) to script story interaction, or use the included [TwineTextPlayer](#twinetextplayer)


#####Exporting .twee files from Twine
######For Twine 1:

1. File > Export > Twee Source Code...
2. Save to a location inside your Unity project.

######For Twine 2:
Requires the [Entweedle](http://www.maximumverbosity.net/twine/Entweedle/) story format.

1. Click the "Formats" link in Twine, then "Add a New Format" and enter this URL: `http://www.maximumverbosity.net/twine/Entweedle/format.js`
2. In your story, select Entweedle as your story format.
3. Press 'Play'
4. Copy and paste the resulting text into an empty text file with the .twee extension. Put this file in your Unity project.

##Documentation

###Importing
* The UnityTwine asset importer listens for any new .twee files dropped into the project directory, and proceeds to import them.
* The asset importer treats Twee code as logic, translating it into a C# script with a similar structure (and the same file name).
A story can be reimported over and over again as necessary; the C# script will be refreshed.
* The generated script can be added to an object in the scene like a normal Unity script.

####Supported syntax
UnityTwine supports many Twine features, but not all (yet). Here is a list of what works and what doesn't:

#####Links
* Simple: `[[passage]]`
* With link text: `[[text|passage]]`
* With variable setters: `[[text|passage][$var = 123]]`
* With expressions: `[[text|either("a", "b")]]

#####Macros

Macros that work:

* `<<if>>` .. `<<else>>` .. `<<endif>>`
* `<<display>>` (but **not** shorthand form)
* `<<print>>`
* `<<set>>` (both single and multiple variables)

Macros that **don't work yet**:

* `<<remember>>`
* `<<action>>`
* `<<choice>>`
* `<<nobr>>`
* HTML stuff: `<<textinput>>`, `<<radio>`,`<<checkbox>>`, `<<button>>`

#####General

* Strings should use `"double quotes"`, not `'single quotes'`.
* For usage with hooks, passage names should not begin with a number or include non-alphanumeric characters.



###Playback
Each passage in an imported Twine story becomes a function that outputs text or links. Custom scripts can listen for generated output,
displaying it as necessary and controlling which links are used to advance the story.

All imported stories include the following editor properties:

* `AutoPlay`: when true, begins playing the story immediately when the game starts.
* `StartPassage`: indicates which passasge to start playback from (default is `Start`)
* `HookScript`: a Unity script which provides story hooks (see the [hooks](#hooks) section for more info)
* A list of Twine variables used in the story, useful for debugging purposes.

#####TwineTextPlayer
Included in UnityTwine is a prefab and script that can be used to quickly display and interact with a story in a text-only fashion. The prefab is built with Unity UI components (4.6+) to handle text and layout. **To use:**

1. Create a new scene
2. Create an empty game object, call it 'TwineStory'
3. Import your Twine story and drag the generated C# script onto the 'TwineStory' game object
4. Drag the TwineTextPlayer prefab into the scene
5. On the TwineTextPlayer object, drag the 'TwineStory' game object into the 'Story' proprety
6. Play your scene

###Scripting



