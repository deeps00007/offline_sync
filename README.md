# sync_offline_requests

Offline-first HTTP request handling for Flutter.
Automatically queues failed API requests and syncs them when internet connectivity is restored.

## ✨ Features

- Offline-first HTTP requests
- Automatic retry with configurable limits
- SQLite-based persistent queue
- Auto-sync when internet is restored
- FIFO request processing
- Simple, minimal API

## 📦 Installation

Add this to your `pubspec.yaml`:

```yaml
dependencies:
  sync_offline_requests: ^1.0.0

---

### C. Quick Start (this is critical)

This should be **copy-paste runnable**.

```md
## 🚀 Quick Start

Initialize once when your app starts:

```dart
void main() {
  OfflineSync.initialize();
  runApp(const MyApp());
}

await OfflineSync.post(
  url: 'https://example.com/api/data',
  body: {
    'name': 'John',
    'age': 25,
  },
);


---

### D. Explain how it works (short but clear)

```md
## 🧠 How It Works

1. API requests are saved locally in SQLite
2. If internet is unavailable, requests stay queued
3. When connectivity is restored, requests are synced automatically
4. Failed requests are retried up to a maximum limit
5. Successfully synced requests are removed from storage



## 🔄 Manual Sync

```dart
await OfflineSync.syncNow();

final count = await OfflineSync.pendingCount();

---

### F. Limitations (honesty = credibility)

```md
## ⚠️ Limitations

- Currently supports POST, PUT, and DELETE methods
- Designed for JSON-based APIs
- Not intended for large file uploads (v1)

## 🛣️ Roadmap

- GET request support
- Custom headers support
- Background sync
- Conflict resolution strategies
