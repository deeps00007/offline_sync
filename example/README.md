# sync_offline_requests Example

This example application demonstrates how to use the `sync_offline_requests` package to handle offline HTTP requests in a Flutter app.

## 📱 Features Demonstrated

The application shows the following core functionalities:

1.  **Initialization**: Setting up the sync engine with lifecycle callbacks.
2.  **Sending Requests**: How to use `OfflineSync.post()` to send data.
3.  **Real-time Monitoring**: Tracking the number of pending requests in the SQLite queue.
4.  **Manual Management**:
    *   Clearing all pending requests.
    *   Cleaning up only failed requests (those that exceeded retry limits).

## 🛠️ How to Run

1.  **Get Dependencies**:
    ```bash
    flutter pub get
    ```

2.  **Run the App**:
    ```bash
    flutter run
    ```

## 🧪 How to Test Offline Behavior

1.  **Launch the app** on a simulator or real device.
2.  **Turn off** Wi-Fi and Mobile Data (enable Airplane Mode).
3.  Tap **"Send Request"**.
    *   Notice the "Pending requests" count increases.
    *   The request is now safely stored in the local SQLite database.
4.  **Turn on** Wi-Fi / Internet.
    *   Watch the debug console (or app logs).
    *   The app automatically detects connectivity and syncs the queued request.
    *   The "Pending requests" count decreases to 0.

## 🧩 Code Highlights

### Initialization & Callbacks
Located in `main.dart`, we initialize the package and listen to sync events:

```dart
OfflineSync.onSyncStart = () => print("🔄 Sync started");
OfflineSync.onRequestSuccess = (id) => print("✅ Synced: $id");
OfflineSync.onRequestFailure = (id, retry) => print("❌ Failed: $id");
OfflineSync.initialize();
```

### Sending a Request
We send a POST request which is automatically handled based on network status:

```dart
await OfflineSync.post(
  url: "https://jsonplaceholder.typicode.com/posts",
  body: {"title": "Offline Test", "body": "Stored in SQLite"},
);
```

### Managing the Queue
We provide buttons to manage the local queue:

```dart
// Clear all pending requests
await OfflineSync.clearAll();

// Clear only requests that have failed multiple times
await OfflineSync.clearFailedOnly();
```
