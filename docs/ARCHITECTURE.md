# 🏗️ Chip App Architecture

This document describes the architecture and folder structure of the Chip Finance Management App, following **Clean Architecture** principles and industry best practices.

## 📂 Project Structure

```
chip/
├── lib/
│   ├── main.dart                           # Application entry point
│   │
│   ├── core/                               # Core utilities shared across features
│   │   ├── constants/                      # App-wide constants
│   │   │   ├── app_constants.dart          # General app constants
│   │   │   ├── api_constants.dart          # API endpoints and keys
│   │   │   └── db_constants.dart           # Database table/field names
│   │   │
│   │   ├── theme/                          # Theme configuration
│   │   │   ├── app_theme.dart              # Main theme configuration
│   │   │   ├── app_colors.dart             # Color palette (teal theme)
│   │   │   ├── app_text_styles.dart        # Typography styles
│   │   │   └── app_dimensions.dart         # Spacing, padding, margins
│   │   │
│   │   ├── utils/                          # Utility functions
│   │   │   ├── date_utils.dart             # Date formatting & calculations
│   │   │   ├── currency_formatter.dart     # Currency formatting (₹)
│   │   │   ├── validators.dart             # Input validation
│   │   │   └── logger.dart                 # Logging utility
│   │   │
│   │   ├── config/                         # App configuration
│   │   │   ├── app_config.dart             # Environment configs
│   │   │   └── routes.dart                 # Route definitions
│   │   │
│   │   └── errors/                         # Error handling
│   │       ├── failures.dart               # Failure classes
│   │       └── exceptions.dart             # Custom exceptions
│   │
│   ├── features/                           # Feature modules (Clean Architecture)
│   │   │
│   │   ├── home/                           # Home Dashboard Feature
│   │   │   ├── presentation/               # UI Layer
│   │   │   │   ├── screens/
│   │   │   │   │   └── home_screen.dart
│   │   │   │   ├── widgets/
│   │   │   │   │   ├── budget_summary_card.dart
│   │   │   │   │   ├── category_grid.dart
│   │   │   │   │   ├── calendar_week_view.dart
│   │   │   │   │   └── recent_transactions_list.dart
│   │   │   │   └── providers/
│   │   │   │       └── home_provider.dart
│   │   │   │
│   │   │   ├── domain/                     # Business Logic Layer
│   │   │   │   ├── entities/
│   │   │   │   │   └── dashboard_data.dart
│   │   │   │   ├── repositories/
│   │   │   │   │   └── home_repository.dart (abstract)
│   │   │   │   └── usecases/
│   │   │   │       └── get_dashboard_data.dart
│   │   │   │
│   │   │   └── data/                       # Data Layer
│   │   │       ├── models/
│   │   │       │   └── dashboard_data_model.dart
│   │   │       ├── repositories/
│   │   │       │   └── home_repository_impl.dart
│   │   │       └── datasources/
│   │   │           ├── home_local_datasource.dart
│   │   │           └── home_remote_datasource.dart
│   │   │
│   │   ├── transactions/                   # Transactions Feature
│   │   │   ├── presentation/
│   │   │   │   ├── screens/
│   │   │   │   │   ├── add_transaction_screen.dart
│   │   │   │   │   ├── transaction_detail_screen.dart
│   │   │   │   │   └── transaction_list_screen.dart
│   │   │   │   ├── widgets/
│   │   │   │   │   ├── transaction_tile.dart
│   │   │   │   │   ├── transaction_form.dart
│   │   │   │   │   └── amount_input_field.dart
│   │   │   │   └── providers/
│   │   │   │       └── transaction_provider.dart
│   │   │   │
│   │   │   ├── domain/
│   │   │   │   ├── entities/
│   │   │   │   │   └── transaction.dart
│   │   │   │   ├── repositories/
│   │   │   │   │   └── transaction_repository.dart
│   │   │   │   └── usecases/
│   │   │   │       ├── add_transaction.dart
│   │   │   │       ├── update_transaction.dart
│   │   │   │       ├── delete_transaction.dart
│   │   │   │       └── get_transactions.dart
│   │   │   │
│   │   │   └── data/
│   │   │       ├── models/
│   │   │       │   └── transaction_model.dart
│   │   │       ├── repositories/
│   │   │       │   └── transaction_repository_impl.dart
│   │   │       └── datasources/
│   │   │           └── transaction_local_datasource.dart
│   │   │
│   │   ├── budget/                         # Budget Management Feature
│   │   │   ├── presentation/
│   │   │   │   ├── screens/
│   │   │   │   │   ├── budget_screen.dart
│   │   │   │   │   └── set_budget_screen.dart
│   │   │   │   ├── widgets/
│   │   │   │   │   ├── budget_progress_bar.dart
│   │   │   │   │   ├── safe_to_spend_widget.dart
│   │   │   │   │   └── budget_alert_card.dart
│   │   │   │   └── providers/
│   │   │   │       └── budget_provider.dart
│   │   │   │
│   │   │   ├── domain/
│   │   │   │   ├── entities/
│   │   │   │   │   └── budget.dart
│   │   │   │   ├── repositories/
│   │   │   │   │   └── budget_repository.dart
│   │   │   │   └── usecases/
│   │   │   │       ├── set_monthly_budget.dart
│   │   │   │       ├── get_budget_status.dart
│   │   │   │       └── calculate_safe_spend.dart
│   │   │   │
│   │   │   └── data/
│   │   │       ├── models/
│   │   │       │   └── budget_model.dart
│   │   │       ├── repositories/
│   │   │       │   └── budget_repository_impl.dart
│   │   │       └── datasources/
│   │   │           └── budget_local_datasource.dart
│   │   │
│   │   ├── categories/                     # Categories Feature
│   │   │   ├── presentation/
│   │   │   │   ├── screens/
│   │   │   │   │   ├── categories_screen.dart
│   │   │   │   │   └── category_detail_screen.dart
│   │   │   │   ├── widgets/
│   │   │   │   │   ├── category_card.dart
│   │   │   │   │   ├── category_icon.dart
│   │   │   │   │   └── add_category_button.dart
│   │   │   │   └── providers/
│   │   │   │       └── category_provider.dart
│   │   │   │
│   │   │   ├── domain/
│   │   │   │   ├── entities/
│   │   │   │   │   └── category.dart
│   │   │   │   ├── repositories/
│   │   │   │   │   └── category_repository.dart
│   │   │   │   └── usecases/
│   │   │   │       ├── get_categories.dart
│   │   │   │       ├── get_category_spending.dart
│   │   │   │       └── create_category.dart
│   │   │   │
│   │   │   └── data/
│   │   │       ├── models/
│   │   │       │   └── category_model.dart
│   │   │       ├── repositories/
│   │   │       │   └── category_repository_impl.dart
│   │   │       └── datasources/
│   │   │           └── category_local_datasource.dart
│   │   │
│   │   ├── analytics/                      # Analytics & Statistics Feature
│   │   │   ├── presentation/
│   │   │   │   ├── screens/
│   │   │   │   │   └── analytics_screen.dart
│   │   │   │   ├── widgets/
│   │   │   │   │   ├── spending_chart.dart
│   │   │   │   │   ├── trend_graph.dart
│   │   │   │   │   └── insights_card.dart
│   │   │   │   └── providers/
│   │   │   │       └── analytics_provider.dart
│   │   │   │
│   │   │   ├── domain/
│   │   │   │   ├── entities/
│   │   │   │   │   └── analytics_data.dart
│   │   │   │   ├── repositories/
│   │   │   │   │   └── analytics_repository.dart
│   │   │   │   └── usecases/
│   │   │   │       ├── get_spending_analytics.dart
│   │   │   │       └── generate_insights.dart
│   │   │   │
│   │   │   └── data/
│   │   │       ├── models/
│   │   │       │   └── analytics_data_model.dart
│   │   │       ├── repositories/
│   │   │       │   └── analytics_repository_impl.dart
│   │   │       └── datasources/
│   │   │           └── analytics_datasource.dart
│   │   │
│   │   └── profile/                        # User Profile Feature
│   │       ├── presentation/
│   │       │   ├── screens/
│   │       │   │   ├── profile_screen.dart
│   │       │   │   └── settings_screen.dart
│   │       │   ├── widgets/
│   │       │   │   ├── profile_header.dart
│   │       │   │   └── settings_tile.dart
│   │       │   └── providers/
│   │       │       └── profile_provider.dart
│   │       │
│   │       ├── domain/
│   │       │   ├── entities/
│   │       │   │   └── user_profile.dart
│   │       │   ├── repositories/
│   │       │   │   └── profile_repository.dart
│   │       │   └── usecases/
│   │       │       ├── get_user_profile.dart
│   │       │       └── update_user_profile.dart
│   │       │
│   │       └── data/
│   │           ├── models/
│   │           │   └── user_profile_model.dart
│   │           ├── repositories/
│   │           │   └── profile_repository_impl.dart
│   │           └── datasources/
│   │               └── profile_local_datasource.dart
│   │
│   └── shared/                             # Shared components across features
│       ├── widgets/                        # Reusable UI components
│       │   ├── custom_button.dart
│       │   ├── custom_text_field.dart
│       │   ├── loading_indicator.dart
│       │   ├── error_widget.dart
│       │   └── bottom_nav_bar.dart
│       │
│       ├── extensions/                     # Dart extensions
│       │   ├── string_extensions.dart
│       │   ├── datetime_extensions.dart
│       │   └── num_extensions.dart
│       │
│       └── services/                       # Shared services
│           ├── database_service.dart       # SQLite/Hive setup
│           ├── notification_service.dart   # Local notifications
│           ├── storage_service.dart        # Shared preferences
│           └── export_service.dart         # PDF/CSV export
│
├── assets/                                 # Static assets
│   ├── images/                            # Image files
│   │   └── logo.png
│   ├── icons/                             # Icon files
│   │   ├── food_icon.png
│   │   ├── travel_icon.png
│   │   └── bills_icon.png
│   └── fonts/                             # Custom fonts
│       └── custom_font.ttf
│
├── test/                                   # Unit & Widget tests
│   ├── features/
│   │   ├── transactions/
│   │   │   ├── domain/
│   │   │   └── data/
│   │   └── budget/
│   └── shared/
│
├── integration_test/                       # Integration tests
│   └── app_test.dart
│
├── android/                                # Android native code
├── ios/                                    # iOS native code
├── web/                                    # Web files
│
├── pubspec.yaml                           # Dependencies
├── analysis_options.yaml                  # Linter rules
├── README.md                              # Project documentation
└── ARCHITECTURE.md                        # This file
```

## 🏛️ Clean Architecture Layers

### 1️⃣ **Presentation Layer** (`presentation/`)
- **Screens**: Full-page views
- **Widgets**: Reusable UI components specific to the feature
- **Providers**: State management (Provider/Riverpod/Bloc)

**Responsibilities:**
- Display data
- Handle user interactions
- Trigger use cases
- React to state changes

### 2️⃣ **Domain Layer** (`domain/`)
- **Entities**: Business objects (pure Dart classes)
- **Repositories**: Abstract contracts (interfaces)
- **Use Cases**: Single-purpose business logic operations

**Responsibilities:**
- Define business rules
- Independent of frameworks
- No dependencies on outer layers

### 3️⃣ **Data Layer** (`data/`)
- **Models**: Data transfer objects that extend entities
- **Repositories**: Concrete implementations
- **Data Sources**: Local (SQLite/Hive) or Remote (API) data access

**Responsibilities:**
- Fetch data from sources
- Convert models to entities
- Handle data persistence

## 🔄 Data Flow

```
User Action → Widget → Provider → Use Case → Repository (Interface) → 
Repository (Implementation) → Data Source → Database/API

Database/API → Data Source → Repository → Use Case → Provider → 
Widget → UI Update
```

## 📱 Feature Organization

Each feature follows the same structure:

```
feature_name/
├── presentation/    # UI components & state management
├── domain/         # Business logic & entities
└── data/           # Data access & models
```

## 🎯 Key Principles

### 1. **Separation of Concerns**
Each layer has a single responsibility and doesn't know about implementation details of other layers.

### 2. **Dependency Rule**
Dependencies point inward. Domain layer is the most stable, presentation is the most volatile.

```
Presentation → Domain ← Data
```

### 3. **Testability**
- Domain layer is 100% testable (pure business logic)
- Data layer is testable with mocks
- Presentation layer tested with widget tests

### 4. **Scalability**
- Easy to add new features without affecting existing code
- Each feature is independent
- Shared code is minimal and well-organized

### 5. **Maintainability**
- Clear structure makes codebase easy to navigate
- Changes are localized to specific layers
- New developers can onboard quickly

## 🔧 State Management

Recommended: **Riverpod** or **Provider**

```dart
// Example Provider structure
lib/features/transactions/presentation/providers/
├── transaction_provider.dart
├── transaction_state.dart
└── transaction_notifier.dart
```

## 🗄️ Database Structure

**SQLite Tables:**

1. **transactions**
   - id (PRIMARY KEY)
   - amount (REAL)
   - category_id (FOREIGN KEY)
   - type (TEXT: 'income' | 'expense')
   - description (TEXT)
   - date (TEXT)
   - created_at (TEXT)

2. **categories**
   - id (PRIMARY KEY)
   - name (TEXT)
   - icon (TEXT)
   - color (TEXT)
   - type (TEXT)

3. **budgets**
   - id (PRIMARY KEY)
   - amount (REAL)
   - month (TEXT)
   - year (INTEGER)

4. **user_profile**
   - id (PRIMARY KEY)
   - name (TEXT)
   - email (TEXT)
   - points (INTEGER)

## 🚀 Best Practices

### File Naming
- Use snake_case: `transaction_list_screen.dart`
- Suffix with purpose: `*_screen.dart`, `*_widget.dart`, `*_provider.dart`

### Code Organization
- One class per file
- Group related files in directories
- Keep files under 300 lines when possible

### Import Order
1. Dart SDK imports
2. Flutter imports
3. Third-party package imports
4. Local imports (core → features → shared)

```dart
import 'dart:async';

import 'package:flutter/material.dart';

import 'package:provider/provider.dart';
import 'package:intl/intl.dart';

import 'package:chip/core/theme/app_colors.dart';
import 'package:chip/features/transactions/domain/entities/transaction.dart';
import 'package:chip/shared/widgets/custom_button.dart';
```

### Documentation
- Document all public APIs
- Add comments for complex business logic
- Use `///` for documentation comments

## 🧪 Testing Strategy

```
test/
├── unit/           # Domain & data layer tests
├── widget/         # Widget tests
└── integration/    # Full app flow tests
```

**Coverage Goals:**
- Domain layer: 100%
- Data layer: 90%+
- Presentation: 70%+

## 📦 Dependency Management

**Core Dependencies:**
- `flutter_riverpod` - State management
- `sqflite` - Local database
- `intl` - Internationalization
- `fl_chart` - Charts
- `shared_preferences` - Simple storage

**Dev Dependencies:**
- `flutter_test`
- `mockito`
- `build_runner`
- `flutter_lints`

## 🔐 Security Considerations

1. **Local Data Encryption**: Encrypt sensitive transaction data
2. **Input Validation**: Validate all user inputs
3. **Secure Storage**: Use `flutter_secure_storage` for sensitive keys
4. **Code Obfuscation**: Enable for production builds

## 📈 Performance Optimization

1. **Lazy Loading**: Load data on demand
2. **Pagination**: For transaction lists
3. **Caching**: Cache frequently accessed data
4. **Image Optimization**: Use WebP format
5. **Build Splitting**: Use const constructors

## 🌐 Internationalization (Future)

```
lib/core/
└── l10n/
    ├── app_en.arb
    ├── app_es.arb
    └── app_hi.arb
```

## 🎨 Theme System

All theme-related code lives in `core/theme/`:
- Colors: Teal-based palette
- Typography: Material Design type scale
- Dimensions: Consistent spacing system

## 📱 Navigation

Using named routes defined in `core/config/routes.dart`:

```dart
static const String home = '/';
static const String addTransaction = '/add-transaction';
static const String analytics = '/analytics';
static const String profile = '/profile';
```

## 🤝 Contributing Guidelines

When adding new features:

1. Follow the clean architecture structure
2. Create feature folder with 3 layers
3. Write tests first (TDD)
4. Update this documentation
5. Follow naming conventions
6. Run linter before committing

---

**This architecture ensures:**
- ✅ Scalability
- ✅ Maintainability  
- ✅ Testability
- ✅ Clean separation of concerns
- ✅ Easy onboarding for new developers
- ✅ Industry-standard practices
