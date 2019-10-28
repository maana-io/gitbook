# Audio Translation

**Material Development Checklist**

* [ ] Power Point Slides \(**not needed**\)
* [x] Workspaces \([https://lastknowngood.knowledge.maana.io/workspace/37ae5256-9486-455c-b4a9-a4d76784a5ad](https://lastknowngood.knowledge.maana.io/workspace/37ae5256-9486-455c-b4a9-a4d76784a5ad)\)
* [x] Step-by-Step Instructions for Learning Assistant \(**completed**\)
* [x] Case description \(**completed**\)
* [x] Recording \(**completed**\)

---------------------------------------------------------------------------------------------------------------

Link to workspace:

{% embed url="https://lastknowngood.knowledge.maana.io/workspace/37ae5256-9486-455c-b4a9-a4d76784a5ad" %}



**Use Case Description:**  

This example demonstrates how the Maana Q platform can be leveraged to extract and transcribe \(and translate\) audio from a video.  In this case we use YouTube as our video source.   With video content being more wide spread the ability to extract knowledge from them could prove vitally important.  Imagine a set of Dr, Patient video consultation or a set of video lectures and what knowledge would be contained in them. 

**Step by Step Instructions:** 

Step 1: Create new workspace and rename 

1. Click on the + icon in the workspace tab, on the left hand side 
2. In the workspace details panel give the workspace a new name -&gt; “Audio Translation” 
3. Click the save icon  

Step 2: Create “top level” function 

Above the canvas click on the create function button, a green function box will appear.  

1. Give the function a name e.g “translateYouTube”.  
2. Add kinds UrlAsInput and FolderAsInput 
3. Edit the function to have youtubeUrl and targetFolder as inputs with the above kinds as types 
4. Click Save

Step 3: Import services to be used and wire up the functions 

1. search for “maana” in the top search bar 
2. drag the following services into the inventory 
3. maana-media-youtube-audio-splitting 
4. maana-azure-speech-to-text 
5. maana-azure-ai-translation-helper 
6. add the following functions to the function graph 
7. getAudioFromYouTubeVideo 
8. transcribeAudio \(from the speech to text service\) 
9. translate \(from the translation helper\) 
10. getEnglishLanguage \(from the translation helper\) 
11. Wire up the functions in the following order 
12. audio splitting -&gt; transcribeAudio -&gt; translate \(with language as 2nd input\) 

Step 4: Test the top level function with GraphQL IDE 

1. Click on the workspace, the graphQL editor will appear in the bottom panel 
2. Type the following into the left hand pane of the editor 

`{` 

 `translateYouTube(` 

   `youtubeUrl:` 

       `{id: "`[`https://www.youtube.com/watch?v=1aA1WGON49E`](https://www.youtube.com/watch?v=1aA1WGON49E)`"},` 

   `targetFolder:` 

       `{id: "`[`http://maana-uploader.azurefd.net/upload`](http://maana-uploader.azurefd.net/upload)`"})` 

`}` 

3. Click Run 

4.Observe output 

Recording: [https://maanainc.app.box.com/folder/91255070799](https://maanainc.app.box.com/folder/91255070799)

