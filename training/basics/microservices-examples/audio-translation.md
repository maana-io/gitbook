---
description: Learn how to compose functions from multiple microservices
---

# Video Translation

**Use Case Description:**  

This example demonstrates how the Maana Q platform can be leveraged to extract and transcribe \(and translate\) audio from a video.  In this case we use YouTube as our video source.   With video content being more wide spread the ability to extract knowledge from them could prove vitally important.  Imagine a set of Dr, Patient video consultation or a set of video lectures and what knowledge would be contained in them. 

**Step by Step Instructions:** 

**Step 1: Examine the function \`translateYouTube\`**

We are going to build a function that will take to arguments: a URL \(which would point to the video we'll translate\) and a target language. The **URL** kind is defined as part of the **Maana Q Common** service, which includes description for commonly used kinds.

Similarly, the concept of a Language Tag \(i.e. "en-US", "de", "it", "he" etc\) is described in the common ontology. The expected output of the function is going to be the translated transcription of the YouTube video.

**Step 2:** **Examine the inventory**

In the inventory, you'll find a list of services that are already imported to the workspace.

1. Maana Q Common - This is the Maana Q Common ontology which includes concepts like URL, Location, Country, State etc - that are commonly used in solutions built on Maana Q.
2. Maana Q Common - Media - This is another ontology that is shared by services dealing with media concepts like File, Audio and Video.

These next set of services are known as "wrappers", and they provide methods that would in turn use available APIs to provide

1. Maana A/V Processing - provides methods for processing audio and video.
2. Maana Audio Transcription - provides methods for transcribing audio.
3. Maana Translation - provides methods for translating text to a desired language
4. Uploader - this utility service that is required for uploading data to a storage solution.
5. YouTube Downloader - this utility service is used to download videos from YouTube.

**Step 3:** **Decomposition**

In order to get the translated text for a YouTube we will need to get the audio from the YouTube video, then transcribe the audio, and finally translate the transcription. Let's add the following functions from the inventory:

1. getAudioFromYouTubeVideo
2. transcribeAudio
3. translate

**Step 4: Implement \`getAudioFromYouTubeVideo\`**

Expand the function `getAudioFromYouTubeVideo`.

1. Add the function `downloadYouTubeVideo`
2. Add the function `splitAudioFromVideo`
3. Wire the functions a\) From the fields `url` and `targetFolder` on the input node to the corresponding fields on the `downloadYouTubeVideo` function b\) From the `targetFolder` on the input node to corresponding filed on the `splitAudioFromVideo` function c\) From the `Video` output of the `downloadYouTubeVideo` to the `video` field on the `splitAudioFromVideo` d\) from the `Audio` output of the `splitAudioFromVideo` to the output node.

**Step 5: Implement the functions**

1. In the explorer panel, click on the function `translate`
2. From the Maana Translation service in your inventory, drag in the function `translate` into your canvas, and wire the function up.
3. In the explorer panel, click on the function `transcribeAudio`
4. From the Maana Audio Transcription service, drag in the function `transcribeAudio`, and wire the function up.
5. In the explorer panel, click on the function `splitAudioFromVideo`
6. From the Maana A/V Processing service, drag in the function `splitAudioFromVideo`, and wire the function up.



