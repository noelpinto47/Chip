# 🔤 Fonts in Chip App

## 📚 Installed Fonts

### 1. **Inter** (Primary Font)
- **Type**: Variable Font
- **File**: `assets/fonts/Inter/Inter-VariableFont_opsz,wght.ttf`
- **Usage**: Default app font for all text
- **Features**: 
  - Supports weight range: 100-900
  - Supports optical sizing
  - Excellent readability for UI text
  - Modern, clean, professional appearance

### 2. **Nunito Sans** (Secondary Font)
- **Type**: Variable Font  
- **File**: `assets/fonts/Nunito_Sans/NunitoSans-VariableFont_YTLC,opsz,wdth,wght.ttf`
- **Usage**: Optional for specific use cases (headings, special text)
- **Features**:
  - Supports weight range
  - Supports optical sizing, width variations
  - Friendly, rounded appearance
  - Great for headings and emphasis

## 💻 Usage in Code

### Default Font (Inter)
The Inter font is set as the default `fontFamily` in `AppTheme`, so all text automatically uses it:

```dart
Text('This uses Inter font by default')
```

### Using Nunito Sans
To use Nunito Sans for specific text:

```dart
Text(
  'Special Heading',
  style: TextStyle(fontFamily: 'NunitoSans'),
)
```

### Using Variable Font Weights
Since these are variable fonts, you can use any weight value:

```dart
// Inter with custom weight
Text(
  'Custom Weight Text',
  style: TextStyle(
    fontFamily: 'Inter',
    fontWeight: FontWeight.w350, // Any value between 100-900
  ),
)

// Or use standard weights
Text(
  'Bold Text',
  style: TextStyle(
    fontFamily: 'Inter',
    fontWeight: FontWeight.bold, // 700
  ),
)
```

## 🎨 Font in Theme

The Inter font is configured in `lib/core/theme/app_theme.dart`:

```dart
ThemeData(
  fontFamily: 'Inter', // Default font
  textTheme: TextTheme(
    // All text styles use Inter by default
    displayLarge: TextStyle(...),
    bodyMedium: TextStyle(...),
    // etc.
  ),
)
```

## 📝 pubspec.yaml Configuration

```yaml
flutter:
  fonts:
    - family: Inter
      fonts:
        - asset: assets/fonts/Inter/Inter-VariableFont_opsz,wght.ttf
    
    - family: NunitoSans
      fonts:
        - asset: assets/fonts/Nunito_Sans/NunitoSans-VariableFont_YTLC,opsz,wdth,wght.ttf
```

## 🎯 Recommended Usage

### Inter (Primary)
- ✅ Body text
- ✅ Button labels
- ✅ Input fields
- ✅ Navigation labels
- ✅ Transaction amounts
- ✅ General UI text

### Nunito Sans (Secondary - Optional)
- ✅ Large headings
- ✅ Welcome messages
- ✅ Onboarding screens
- ✅ Special callouts
- ✅ Marketing content

## 🔧 Variable Font Benefits

1. **Single File**: One file contains all weights (saves app size)
2. **Smooth Scaling**: Interpolate between weights smoothly
3. **Custom Weights**: Use any weight value (100-900), not just predefined
4. **Better Performance**: Less font loading overhead

## 🌟 Font Weight Reference

```dart
FontWeight.w100  // Thin
FontWeight.w200  // Extra Light
FontWeight.w300  // Light
FontWeight.w400  // Regular (normal)
FontWeight.w500  // Medium
FontWeight.w600  // Semi Bold
FontWeight.w700  // Bold
FontWeight.w800  // Extra Bold
FontWeight.w900  // Black
```

## 🎨 Examples in Chip App

### Budget Amount
```dart
Text(
  '₹18,000',
  style: TextStyle(
    fontFamily: 'Inter',
    fontSize: 32,
    fontWeight: FontWeight.w700,
    fontFeatures: [FontFeature.tabularFigures()],
  ),
)
```

### Category Name
```dart
Text(
  'Food',
  style: TextStyle(
    fontFamily: 'Inter',
    fontSize: 14,
    fontWeight: FontWeight.w500,
  ),
)
```

### Greeting (Optional with Nunito Sans)
```dart
Text(
  'Hello, Noel',
  style: TextStyle(
    fontFamily: 'NunitoSans',
    fontSize: 24,
    fontWeight: FontWeight.w600,
  ),
)
```

## ✅ Verification

After running `flutter pub get`, verify fonts are working:

1. Run the app: `flutter run`
2. Check if text appears in Inter font
3. Look for smooth, modern typography
4. No fallback to system fonts

## 📦 Font Files Info

- **Inter**: Google Fonts, Open Font License
- **Nunito Sans**: Google Fonts, Open Font License
- Both are free for commercial use
- Variable fonts for optimal performance

---

**Your app now has professional, modern typography! 🎉**
