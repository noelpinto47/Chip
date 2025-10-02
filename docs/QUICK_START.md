# 🚀 Quick Start - Final Setup (35 Minutes)

Before starting development, complete these 3 essential configurations:

---

## ⏱️ Step 1: Change Package Name (5 minutes)

### Android Package Name

**File:** `android/app/build.gradle.kts`

Change from:
```gradle
applicationId = "com.example.chip"
```

To:
```gradle
applicationId = "com.noelpinto.chip"  // Or your preferred domain
```

### Why?
- Required for Play Store publication
- Must be unique globally
- Cannot be changed after publishing

---

## ⏱️ Step 2: Add State Management (10 minutes)

### Install Riverpod

```bash
flutter pub add flutter_riverpod
```

### Update main.dart

Wrap your app with ProviderScope:

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

void main() {
  runApp(
    const ProviderScope(  // Add this wrapper
      child: ChipApp(),
    ),
  );
}
```

### Why?
- Manage app state efficiently
- Handle business logic
- Update UI reactively
- Industry standard for Flutter

---

## ⏱️ Step 3: Add Database (20 minutes)

### Install Packages

```bash
flutter pub add sqflite path_provider path
```

### Create Database Service

**File:** `lib/shared/services/database_service.dart`

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

class DatabaseService {
  static Database? _database;
  static const String dbName = 'chip_database.db';
  static const int dbVersion = 1;

  Future<Database> get database async {
    if (_database != null) return _database!;
    _database = await _initDatabase();
    return _database!;
  }

  Future<Database> _initDatabase() async {
    final dbPath = await getDatabasesPath();
    final path = join(dbPath, dbName);

    return await openDatabase(
      path,
      version: dbVersion,
      onCreate: _onCreate,
    );
  }

  Future<void> _onCreate(Database db, int version) async {
    // Transactions table
    await db.execute('''
      CREATE TABLE transactions(
        id TEXT PRIMARY KEY,
        amount REAL NOT NULL,
        category_id TEXT NOT NULL,
        type TEXT NOT NULL,
        description TEXT NOT NULL,
        date TEXT NOT NULL,
        created_at TEXT NOT NULL
      )
    ''');

    // Categories table
    await db.execute('''
      CREATE TABLE categories(
        id TEXT PRIMARY KEY,
        name TEXT NOT NULL,
        icon TEXT NOT NULL,
        color TEXT NOT NULL,
        type TEXT NOT NULL
      )
    ''');

    // Budgets table
    await db.execute('''
      CREATE TABLE budgets(
        id TEXT PRIMARY KEY,
        amount REAL NOT NULL,
        month INTEGER NOT NULL,
        year INTEGER NOT NULL,
        created_at TEXT NOT NULL
      )
    ''');

    // Insert default categories
    await _insertDefaultCategories(db);
  }

  Future<void> _insertDefaultCategories(Database db) async {
    final categories = [
      {'id': '1', 'name': 'Food', 'icon': '🍔', 'color': 'FF9800', 'type': 'food'},
      {'id': '2', 'name': 'Travel', 'icon': '✈️', 'color': '2196F3', 'type': 'travel'},
      {'id': '3', 'name': 'Bills', 'icon': '📄', 'color': 'E91E63', 'type': 'bills'},
      {'id': '4', 'name': 'Savings', 'icon': '💰', 'color': '4CAF50', 'type': 'savings'},
    ];

    for (final category in categories) {
      await db.insert('categories', category);
    }
  }
}
```

### Why?
- Store transactions locally
- Work offline
- Fast data access
- Essential for finance app

---

## ✅ Verification Commands

After completing all steps:

```bash
# Clean build
flutter clean

# Get dependencies
flutter pub get

# Run app
flutter run
```

---

## 🎯 After These 3 Steps...

You'll be **100% ready** to start development! 

**Next:** Begin building the Transaction feature:
1. Create `Transaction` entity
2. Create `Category` entity  
3. Build Add Transaction screen
4. Implement CRUD operations

---

## 📝 Quick Reference

**Package Name:** Change in `android/app/build.gradle.kts`  
**State Management:** `flutter pub add flutter_riverpod`  
**Database:** `flutter pub add sqflite path_provider path`  

**Total Time:** ~35 minutes  
**Result:** Production-ready foundation! 🚀

---

Run these commands now:

```bash
# Step 1: Manual edit (android/app/build.gradle.kts)

# Step 2: Add Riverpod
flutter pub add flutter_riverpod

# Step 3: Add Database
flutter pub add sqflite path_provider path

# Get all dependencies
flutter pub get

# You're ready!
flutter run
```

🎉 **Happy Coding!**
