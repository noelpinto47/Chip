# 🚀 Getting Started with Chip Development

## 📋 Current Status

✅ **Directory structure created** - Clean Architecture compliant  
✅ **Core utilities implemented** - Theme, Colors, Utils  
✅ **Feature modules scaffolded** - 6 main features ready  
⏳ **Pending** - Dependencies, Entity models, Database setup  

---

## 🎯 Immediate Next Steps

### Step 1: Install Required Dependencies

Update your `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  
  # State Management
  flutter_riverpod: ^2.4.0
  
  # Local Database
  sqflite: ^2.3.0
  path: ^1.8.3
  path_provider: ^2.1.0
  
  # Date & Currency Formatting
  intl: ^0.18.1
  
  # Simple Storage
  shared_preferences: ^2.2.2
  
  # Charts
  fl_chart: ^0.66.0
  
  # UI Enhancements
  flutter_slidable: ^3.0.0
  shimmer: ^3.0.0
  
  # Notifications
  flutter_local_notifications: ^16.0.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^3.0.0
  mockito: ^5.4.4
  build_runner: ^2.4.7
```

**Run:**
```bash
flutter pub get
```

---

### Step 2: Create Core Entities

Create these entity files first:

#### 📄 `lib/features/transactions/domain/entities/transaction.dart`
```dart
class Transaction {
  final String id;
  final double amount;
  final String categoryId;
  final TransactionType type;
  final String description;
  final DateTime date;
  final DateTime createdAt;

  Transaction({
    required this.id,
    required this.amount,
    required this.categoryId,
    required this.type,
    required this.description,
    required this.date,
    required this.createdAt,
  });
}

enum TransactionType { income, expense }
```

#### 📄 `lib/features/categories/domain/entities/category.dart`
```dart
class Category {
  final String id;
  final String name;
  final String icon;
  final String color;
  final CategoryType type;

  Category({
    required this.id,
    required this.name,
    required this.icon,
    required this.color,
    required this.type,
  });
}

enum CategoryType { food, travel, bills, savings, other }
```

#### 📄 `lib/features/budget/domain/entities/budget.dart`
```dart
class Budget {
  final String id;
  final double amount;
  final int month;
  final int year;
  final DateTime createdAt;

  Budget({
    required this.id,
    required this.amount,
    required this.month,
    required this.year,
    required this.createdAt,
  });
}
```

---

### Step 3: Set Up Database

Create `lib/shared/services/database_service.dart`:

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
    // Create tables
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

    await db.execute('''
      CREATE TABLE categories(
        id TEXT PRIMARY KEY,
        name TEXT NOT NULL,
        icon TEXT NOT NULL,
        color TEXT NOT NULL,
        type TEXT NOT NULL
      )
    ''');

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

---

### Step 4: Update main.dart

Update `lib/main.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'core/theme/app_theme.dart';

void main() {
  runApp(
    const ProviderScope(
      child: ChipApp(),
    ),
  );
}

class ChipApp extends StatelessWidget {
  const ChipApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Chip - Finance Management',
      theme: AppTheme.lightTheme,
      debugShowCheckedModeBanner: false,
      home: const HomeScreen(), // Create this next
    );
  }
}
```

---

### Step 5: Create Home Screen Scaffold

Create `lib/features/home/presentation/screens/home_screen.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:chip/core/theme/app_colors.dart';

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  int _currentIndex = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Hello, Noel'),
        actions: [
          IconButton(
            icon: const Icon(Icons.notifications_outlined),
            onPressed: () {},
          ),
        ],
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            // TODO: Add Budget Card
            // TODO: Add Calendar Widget
            // TODO: Add Category Grid
            // TODO: Add Recent Transactions
          ],
        ),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _currentIndex,
        onTap: (index) => setState(() => _currentIndex = index),
        type: BottomNavigationBarType.fixed,
        selectedItemColor: AppColors.primary,
        items: const [
          BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Home'),
          BottomNavigationBarItem(icon: Icon(Icons.analytics), label: 'Analytics'),
          BottomNavigationBarItem(icon: Icon(Icons.category), label: 'Categories'),
          BottomNavigationBarItem(icon: Icon(Icons.person), label: 'Profile'),
        ],
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // TODO: Navigate to Add Transaction
        },
        child: const Icon(Icons.add),
      ),
      floatingActionButtonLocation: FloatingActionButtonLocation.centerDocked,
    );
  }
}
```

---

### Step 6: Create Your First Widget

Create `lib/features/home/presentation/widgets/budget_summary_card.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:chip/core/theme/app_colors.dart';
import 'package:chip/core/theme/app_dimensions.dart';
import 'package:chip/core/utils/currency_formatter.dart';

class BudgetSummaryCard extends StatelessWidget {
  final double spent;
  final double budget;
  final String month;

  const BudgetSummaryCard({
    super.key,
    required this.spent,
    required this.budget,
    required this.month,
  });

  @override
  Widget build(BuildContext context) {
    final percentage = budget > 0 ? spent / budget : 0.0;
    final safeToSpend = budget - spent;
    final daysRemaining = 30 - DateTime.now().day;
    final dailySafe = daysRemaining > 0 ? safeToSpend / daysRemaining : 0.0;

    return Card(
      child: Padding(
        padding: const EdgeInsets.all(AppDimensions.paddingLarge),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(month, style: Theme.of(context).textTheme.titleMedium),
            const SizedBox(height: AppDimensions.spaceMedium),
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: [
                Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text('You\'ve Spent', 
                      style: Theme.of(context).textTheme.bodySmall),
                    Text(CurrencyFormatter.format(spent),
                      style: Theme.of(context).textTheme.headlineMedium),
                  ],
                ),
                Column(
                  crossAxisAlignment: CrossAxisAlignment.end,
                  children: [
                    Text('Budget',
                      style: Theme.of(context).textTheme.bodySmall),
                    Text(CurrencyFormatter.format(budget),
                      style: Theme.of(context).textTheme.headlineMedium),
                  ],
                ),
              ],
            ),
            const SizedBox(height: AppDimensions.spaceMedium),
            LinearProgressIndicator(
              value: percentage,
              minHeight: AppDimensions.progressBarHeight,
              backgroundColor: AppColors.progressBackground,
              valueColor: const AlwaysStoppedAnimation(AppColors.progressFill),
            ),
            const SizedBox(height: AppDimensions.spaceSmall),
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: [
                Text('${(percentage * 100).toInt()}% used',
                  style: Theme.of(context).textTheme.bodyMedium),
                Text('Safe to spend: ${CurrencyFormatter.format(dailySafe)}/day',
                  style: Theme.of(context).textTheme.bodySmall),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## 📝 Development Workflow

### Daily Development:
1. Pick a feature to implement
2. Start with domain layer (entities, use cases)
3. Implement data layer (models, repositories)
4. Build presentation layer (UI, widgets)
5. Write tests
6. Commit changes

### Recommended Order:
1. ✅ Set up database (Step 3)
2. ✅ Create core entities (Step 2)
3. 🔄 Implement Transactions feature
4. 🔄 Implement Budget feature
5. 🔄 Implement Categories feature
6. 🔄 Implement Home dashboard
7. 🔄 Implement Analytics
8. 🔄 Implement Profile

---

## 🧪 Testing

Create tests in `test/` folder:

```
test/
├── features/
│   ├── transactions/
│   │   ├── domain/
│   │   └── data/
│   └── budget/
└── core/
    └── utils/
```

Run tests:
```bash
flutter test
```

---

## 🐛 Debugging Tips

- Use `AppLogger` for debugging: `AppLogger.debug('Message', 'TAG')`
- Check database with: `adb shell` → `run-as com.yourapp` → `sqlite3 databases/chip_database.db`
- Hot reload: `r` in terminal
- Hot restart: `R` in terminal

---

## 📚 Resources

- **Flutter Docs**: https://flutter.dev/docs
- **Riverpod**: https://riverpod.dev
- **SQLite**: https://pub.dev/packages/sqflite
- **Clean Architecture**: See `ARCHITECTURE.md`

---

## ✅ Checklist

Before starting development:
- [ ] Install dependencies (`flutter pub get`)
- [ ] Create entity classes
- [ ] Set up database service
- [ ] Update main.dart with theme
- [ ] Create home screen scaffold
- [ ] Test app runs successfully

---

**You're all set! Start building your Chip app! 🚀💰**

Questions? Check `ARCHITECTURE.md` for detailed documentation.
