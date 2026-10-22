# Instagram Clone (Flutter + Firebase)

An Instagram-style app in Flutter with a Firebase backend, running on Android, iOS and web. I built it in 2022 by following Rivaan Ranawat's Flutter and Firebase Instagram clone tutorial, as a way to learn Firebase Auth, Firestore, Storage and Provider.

## Features

- Email and password sign up (with username, bio and profile photo) and login through Firebase Auth
- Feed of all posts, streamed live from Firestore
- New posts from the camera or gallery, with a caption. Images go to Firebase Storage.
- Likes (button or double tap, with a heart animation), comments, and deleting your own posts
- User search by username, and a grid of all posts on the search tab
- Profiles with post, follower and following counts, follow/unfollow, and sign out
- Responsive layout: bottom tab bar on narrow screens, top nav bar when wider than 600px

The notifications tab is a placeholder.

## Stack

- Flutter (stable channel, Dart `>=2.15.0`) with Provider for the current user state
- `firebase_core` 1.x, `firebase_auth` 3.x, `cloud_firestore` 3.x, `firebase_storage` 10.x
- `image_picker`, `flutter_staggered_grid_view`, `flutter_svg`, `intl`, `uuid`

These are the 2022 versions it was built against. It hasn't been updated for current Flutter or FlutterFire.

## Data model

- `users/{uid}`: uid, username, email, bio, photoUrl, followers, following
- `posts/{postId}`: postId, description, uid, username, likes, datePublished, postUrl, profImage
- `posts/{postId}/comments/{commentId}`
- Storage: `profilePics/{uid}` and `posts/{uid}/{random id}`

## Structure

```
lib/
  models/      User and Post
  providers/   UserProvider
  resources/   auth, Firestore and Storage calls
  responsive/  mobile and web layouts, and the switch between them
  screens/     login, signup, feed, search, add post, comments, profile
  widgets/     post card, comment card, like animation, follow button, text field
```

## Running it

1. Create a Firebase project and enable Email/Password auth, Firestore and Storage.
2. Add Android, iOS and web apps to the project. Replace `android/app/google-services.json` and `ios/Runner/GoogleService-Info.plist` with your own, and swap the `FirebaseOptions` in `lib/main.dart` (used for web) for your web app's config.
3. Run:

```bash
flutter pub get
flutter run              # Android or iOS
flutter run -d chrome    # web
```
