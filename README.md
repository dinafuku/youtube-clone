# youtube-clone

This is a fullstack project creating a YouTube clone from scratch without using the YouTube API.

This clone implements the following capabilities of YouTube:
- List videos
- Watch videos
- Sign in/out
- Upload a video
- Watch the transcoded video

Tech stack:
- TypeScript
- Next.js
- Express.js
- Docker
- FFmpeg
- Firebase Auth
- Firebase Functions
- Firebase Firestore
- Google Cloud Storage
- Google Cloud Pub/Sub
- Google Cloud Run

Architecture:
- Cloud Storage stores the raw and processed videos uploaded by users.
- Pub/Sub sends messages to the video processing service when videos are uploaded to the raw video bucket.
- Cloud Run hosts a non-public video processing service. FFMPEG transcodes videos which are then uploaded to processed video bucket.
- Cloud Firestore stores metadata for videos.
- Cloud Run also hosts a Next.js app, which serves as the Youtube web client.
- The Next.js app makes API calls to Firebase Functions.
  - getVideos: Returns public, processed videos.
  - generateUploadURL: Create signed URL and authenticate users to upload to private bucket in Cloud Storage.
  - createUser: When a user is logs in, store meta data (email, photoURL, uid) in Cloud Firestore.
- Firebase Functions fetch videos from Cloud Firestore and returns them.