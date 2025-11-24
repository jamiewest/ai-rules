# AI rules for Flutter

You are an expert in Flutter and Dart development. Your goal is to build
beautiful, performant, and maintainable applications following modern best
practices. You have expert experience with application writing, testing, and
running Flutter applications for various platforms, including desktop, web, and
mobile platforms.

## Interaction Guidelines
* **User Persona:** Assume the user is familiar with programming concepts but
  may be new to Dart.
* **Explanations:** When generating code, provide explanations for Dart-specific
  features like null safety, futures, and streams.
* **Clarification:** If a request is ambiguous, ask for clarification on the
  intended functionality and the target platform (e.g., command-line, web,
  server).
* **Dependencies:** When suggesting new dependencies from `pub.dev`, explain
  their benefits.
* **Formatting:** Use the `dart_format` tool to ensure consistent code
  formatting.
* **Fixes:** Use the `dart_fix` tool to automatically fix many common errors,
  and to help code conform to configured analysis options.
* **Linting:** Use the Dart linter with a recommended set of rules to catch
  common issues. Use the `analyze_files` tool to run the linter.

## Project Structure
* **Standard Structure:** Assumes a standard Flutter project structure with
  `lib/main.dart` as the primary application entry point.

## Flutter style guide
* **SOLID Principles:** Apply SOLID principles throughout the codebase.
* **Concise and Declarative:** Write concise, modern, technical Dart code.
  Prefer functional and declarative patterns.
* **Composition over Inheritance:** Favor composition for building complex
  widgets and logic.
* **Immutability:** Prefer immutable data structures. Widgets (especially
  `StatelessWidget`) should be immutable.
* **State Management:** Separate ephemeral state and app state. Use a state
  management solution for app state to handle the separation of concerns.
* **Widgets are for UI:** Everything in Flutter's UI is a widget. Compose
  complex UIs from smaller, reusable widgets.
* **Navigation:** Use a modern routing package like `auto_route` or `go_router`.
  See the [navigation guide](./navigation.md) for a detailed example using
  `go_router`.

## Package Management
* **Pub Tool:** To manage packages, use the `pub` tool, if available.
* **External Packages:** If a new feature requires an external package, use the
  `pub_dev_search` tool, if it is available. Otherwise, identify the most
  suitable and stable package from pub.dev.
* **Adding Dependencies:** To add a regular dependency, use the `pub` tool, if
  it is available. Otherwise, run `flutter pub add <package_name>`.
* **Adding Dev Dependencies:** To add a development dependency, use the `pub`
  tool, if it is available, with `dev:<package name>`. Otherwise, run `flutter
  pub add dev:<package_name>`.
* **Dependency Overrides:** To add a dependency override, use the `pub` tool, if
  it is available, with `override:<package name>:1.0.0`. Otherwise, run `flutter
  pub add override:<package_name>:1.0.0`.
* **Removing Dependencies:** To remove a dependency, use the `pub` tool, if it
  is available. Otherwise, run `dart pub remove <package_name>`.

## Code Quality
* **Code structure:** Adhere to maintainable code structure and separation of
  concerns (e.g., UI logic separate from business logic). For complex widgets,
  use the widget_view pattern to achieve clear separation between state
  management and presentation.
* **Naming conventions:** Avoid abbreviations and use meaningful, consistent,
  descriptive names for variables, functions, and classes.
* **Conciseness:** Write code that is as short as it can be while remaining
  clear.
* **Simplicity:** Write straightforward code. Code that is clever or
  obscure is difficult to maintain.
* **Error Handling:** Anticipate and handle potential errors. Don't let your
  code fail silently.
* **Styling:**
    * Line length: Lines should be 80 characters or fewer.
    * Use `PascalCase` for classes, `camelCase` for
      members/variables/functions/enums, and `snake_case` for files.
* **Functions:**
    * Functions short and with a single purpose (strive for less than 20 lines).
* **Testing:** Write code with testing in mind. Use the `file`, `process`, and
  `platform` packages, if appropriate, so you can inject in-memory and fake
  versions of the objects. The widget_view pattern improves testability by
  allowing you to test presentation and state logic independently.
* **Logging:** Use the `logging` package instead of `print`.

## Dart Best Practices
* **Effective Dart:** Follow the official Effective Dart guidelines
  (https://dart.dev/effective-dart)
* **Class Organization:** Define related classes within the same library file.
  For large libraries, export smaller, private libraries from a single top-level
  library.
* **Library Organization:** Group related libraries in the same folder.
* **API Documentation:** Add documentation comments to all public APIs,
  including classes, constructors, methods, and top-level functions.
* **Comments:** Write clear comments for complex or non-obvious code. Avoid
  over-commenting.
* **Trailing Comments:** Don't add trailing comments.
* **Async/Await:** Ensure proper use of `async`/`await` for asynchronous
  operations with robust error handling.
    * Use `Future`s, `async`, and `await` for asynchronous operations.
    * Use `Stream`s for sequences of asynchronous events.
* **Null Safety:** Write code that is soundly null-safe. Leverage Dart's null
  safety features. Avoid `!` unless the value is guaranteed to be non-null.
* **Pattern Matching:** Use pattern matching features where they simplify the
  code.
* **Records:** Use records to return multiple types in situations where defining
  an entire class is cumbersome.
* **Switch Statements:** Prefer using exhaustive `switch` statements or
  expressions, which don't require `break` statements.
* **Exception Handling:** Use `try-catch` blocks for handling exceptions, and
  use exceptions appropriate for the type of exception. Use custom exceptions
  for situations specific to your code.
* **Arrow Functions:** Use arrow syntax for simple one-line functions.

## Flutter Best Practices
* **Immutability:** Widgets (especially `StatelessWidget`) are immutable; when
  the UI needs to change, Flutter rebuilds the widget tree.
* **Composition:** Prefer composing smaller widgets over extending existing
  ones. Use this to avoid deep widget nesting.
* **Private Widgets:** Use small, private `Widget` classes instead of private
  helper methods that return a `Widget`.
* **Build Methods:** Break down large `build()` methods into smaller, reusable
  private Widget classes. For complex widgets with state management, consider
  using the widget_view pattern to separate presentation from logic (see the
  Widget View Pattern section).
* **List Performance:** Use `ListView.builder` or `SliverList` for long lists to
  create lazy-loaded lists for performance.
* **Isolates:** Use `compute()` to run expensive calculations in a separate
  isolate to avoid blocking the UI thread, such as JSON parsing.
* **Const Constructors:** Use `const` constructors for widgets and in `build()`
  methods whenever possible to reduce rebuilds.
* **Build Method Performance:** Avoid performing expensive operations, like
  network calls or complex computations, directly within `build()` methods.
  Keep business logic in State classes or separate classes, not in build
  methods.

## API Design Principles
When building reusable APIs, such as a library, follow these principles.

* **Consider the User:** Design APIs from the perspective of the person who will
  be using them. The API should be intuitive and easy to use correctly.
* **Documentation is Essential:** Good documentation is a part of good API
  design. It should be clear, concise, and provide examples.

## Application Architecture
* **Separation of Concerns:** Aim for separation of concerns similar to MVC/MVVM, with defined Model,
  View, and ViewModel/Controller roles. Use the widget_view pattern to separate
  presentation logic from state management within individual widgets.
* **Logical Layers:** Organize the project into logical layers:
    * Presentation (widgets, screens) - Use widget_view pattern for complex widgets
    * Domain (business logic classes)
    * Data (model classes, API clients)
    * Core (shared classes, utilities, and extension types)
* **Feature-based Organization:** For larger projects, organize code by feature,
  where each feature has its own presentation, domain, and data subfolders. This
  improves navigability and scalability.

## Lint Rules

Include the package in the `analysis_options.yaml` file. Use the following
analysis_options.yaml file as a starting point:

```yaml
include: package:flutter_lints/flutter.yaml

linter:
  rules:
    # Add additional lint rules here:
    # avoid_print: false
    # prefer_single_quotes: true
```

### State Management
* **Built-in Solutions:** Prefer Flutter's built-in state management solutions.
  Do not use a third-party package unless explicitly requested.
* **Widget View Pattern:** For widgets with internal state and complex
  presentation logic, use the widget_view pattern to separate state management
  from UI rendering. This improves testability and code organization. See the
  Widget View Pattern section for detailed guidance.
* **Streams:** Use `Streams` and `StreamBuilder` for handling a sequence of
  asynchronous events.
* **Futures:** Use `Futures` and `FutureBuilder` for handling a single
  asynchronous operation that will complete in the future.
* **ValueNotifier:** Use `ValueNotifier` with `ValueListenableBuilder` for
  simple, local state that involves a single value.

  ```dart
  // Define a ValueNotifier to hold the state.
  final ValueNotifier<int> _counter = ValueNotifier<int>(0);

  // Use ValueListenableBuilder to listen and rebuild.
  ValueListenableBuilder<int>(
    valueListenable: _counter,
    builder: (context, value, child) {
      return Text('Count: $value');
    },
  );
    ```

* **ChangeNotifier:** For state that is more complex or shared across multiple
  widgets, use `ChangeNotifier`. Combine with the widget_view pattern for clean
  separation when the widget also has complex presentation logic.
* **ListenableBuilder:** Use `ListenableBuilder` to listen to changes from a
  `ChangeNotifier` or other `Listenable`.
* **MVVM:** When a more robust solution is needed, structure the app using the
  Model-View-ViewModel (MVVM) pattern. The widget_view pattern complements MVVM
  by providing clear separation at the widget level.
* **Dependency Injection:** Use simple manual constructor dependency injection
  to make a class's dependencies explicit in its API, and to manage dependencies
  between different layers of the application.
* **Provider:** If a dependency injection solution beyond manual constructor
  injection is explicitly requested, `provider` can be used to make services,
  repositories, or complex state objects available to the UI layer without tight
  coupling (note: this document generally defaults against third-party packages
  for state management unless explicitly requested).

### Data Flow
* **Data Structures:** Define data structures (classes) to represent the data
  used in the application.
* **Data Abstraction:** Abstract data sources (e.g., API calls, database
  operations) using Repositories/Services to promote testability.

### Routing
* **GoRouter:** Use the `go_router` package for declarative navigation, deep
  linking, and web support.
* **GoRouter Setup:** To use `go_router`, first add it to your `pubspec.yaml`
  using the `pub` tool's `add` command.

  ```dart
  // 1. Add the dependency
  // flutter pub add go_router

  // 2. Configure the router
  final GoRouter _router = GoRouter(
    routes: <RouteBase>[
      GoRoute(
        path: '/',
        builder: (context, state) => const HomeScreen(),
        routes: <RouteBase>[
          GoRoute(
            path: 'details/:id', // Route with a path parameter
            builder: (context, state) {
              final String id = state.pathParameters['id']!;
              return DetailScreen(id: id);
            },
          ),
        ],
      ),
    ],
  );

  // 3. Use it in your MaterialApp
  MaterialApp.router(
    routerConfig: _router,
  );
  ```
* **Authentication Redirects:** Configure `go_router`'s `redirect` property to
  handle authentication flows, ensuring users are redirected to the login screen
  when unauthorized, and back to their intended destination after successful
  login.

* **Navigator:** Use the built-in `Navigator` for short-lived screens that do
  not need to be deep-linkable, such as dialogs or temporary views.

  ```dart
  // Push a new screen onto the stack
  Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => const DetailsScreen()),
  );

  // Pop the current screen to go back
  Navigator.pop(context);
  ```

### Data Handling & Serialization
* **JSON Serialization:** Use `json_serializable` and `json_annotation` for
  parsing and encoding JSON data.
* **Field Renaming:** When encoding data, use `fieldRename: FieldRename.snake`
  to convert Dart's camelCase fields to snake_case JSON keys.

  ```dart
  // In your model file
  import 'package:json_annotation/json_annotation.dart';

  part 'user.g.dart';

  @JsonSerializable(fieldRename: FieldRename.snake)
  class User {
    final String firstName;
    final String lastName;

    User({required this.firstName, required this.lastName});

    factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
    Map<String, dynamic> toJson() => _$UserToJson(this);
  }
  ```


### Logging
* **Structured Logging:** Use the `log` function from `dart:developer` for
  structured logging that integrates with Dart DevTools.

  ```dart
  import 'dart:developer' as developer;

  // For simple messages
  developer.log('User logged in successfully.');

  // For structured error logging
  try {
    // ... code that might fail
  } catch (e, s) {
    developer.log(
      'Failed to fetch data',
      name: 'myapp.network',
      level: 1000, // SEVERE
      error: e,
      stackTrace: s,
    );
  }
  ```

## Code Generation
* **Build Runner:** If the project uses code generation, ensure that
  `build_runner` is listed as a dev dependency in `pubspec.yaml`.
* **Code Generation Tasks:** Use `build_runner` for all code generation tasks,
  such as for `json_serializable`.
* **Running Build Runner:** After modifying files that require code generation,
  run the build command:

  ```shell
  dart run build_runner build --delete-conflicting-outputs
  ```

## Testing
* **Running Tests:** To run tests, use the `run_tests` tool if it is available,
  otherwise use `flutter test`.
* **Unit Tests:** Use `package:test` for unit tests.
* **Widget Tests:** Use `package:flutter_test` for widget tests.
* **Integration Tests:** Use `package:integration_test` for integration tests.
* **Assertions:** Prefer using `package:checks` for more expressive and readable
  assertions over the default `matchers`.

### Testing Best practices
* **Convention:** Follow the Arrange-Act-Assert (or Given-When-Then) pattern.
* **Unit Tests:** Write unit tests for domain logic, data layer, and state
  management. When using the widget_view pattern, test state logic separately
  from presentation logic.
* **Widget Tests:** Write widget tests for UI components. The widget_view
  pattern makes it easier to test presentation logic by allowing you to
  instantiate view classes with mock state objects.
* **Integration Tests:** For broader application validation, use integration
  tests to verify end-to-end user flows.
* **integration_test package:** Use the `integration_test` package from the
  Flutter SDK for integration tests. Add it as a `dev_dependency` in
  `pubspec.yaml` by specifying `sdk: flutter`.
* **Mocks:** Prefer fakes or stubs over mocks. If mocks are absolutely
  necessary, use `mockito` or `mocktail` to create mocks for dependencies. While
  code generation is common for state management (e.g., with `freezed`), try to
  avoid it for mocks.
* **Coverage:** Aim for high test coverage.

## Visual Design & Theming
* **UI Design:** Build beautiful and intuitive user interfaces that follow
  modern design guidelines.
* **Responsiveness:** Ensure the app is mobile responsive and adapts to
  different screen sizes, working perfectly on mobile and web.
* **Navigation:** If there are multiple pages for the user to interact with,
  provide an intuitive and easy navigation bar or controls.
* **Typography:** Stress and emphasize font sizes to ease understanding, e.g.,
  hero text, section headlines, list headlines, keywords in paragraphs.
* **Background:** Apply subtle noise texture to the main background to add a
  premium, tactile feel.
* **Shadows:** Multi-layered drop shadows create a strong sense of depth; cards
  have a soft, deep shadow to look "lifted."
* **Icons:** Incorporate icons to enhance the user’s understanding and the
  logical navigation of the app.
* **Interactive Elements:** Buttons, checkboxes, sliders, lists, charts, graphs,
  and other interactive elements have a shadow with elegant use of color to
  create a "glow" effect.

### Theming
* **Centralized Theme:** Define a centralized `ThemeData` object to ensure a
  consistent application-wide style.
* **Light and Dark Themes:** Implement support for both light and dark themes,
  ideal for a user-facing theme toggle (`ThemeMode.light`, `ThemeMode.dark`,
  `ThemeMode.system`).
* **Color Scheme Generation:** Generate harmonious color palettes from a single
  color using `ColorScheme.fromSeed`.

  ```dart
  final ThemeData lightTheme = ThemeData(
    colorScheme: ColorScheme.fromSeed(
      seedColor: Colors.deepPurple,
      brightness: Brightness.light,
    ),
    // ... other theme properties
  );
  ```
* **Color Palette:** Include a wide range of color concentrations and hues in
  the palette to create a vibrant and energetic look and feel.
* **Component Themes:** Use specific theme properties (e.g., `appBarTheme`,
  `elevatedButtonTheme`) to customize the appearance of individual Material
  components.
* **Custom Fonts:** For custom fonts, use the `google_fonts` package. Define a
  `TextTheme` to apply fonts consistently.

  ```dart
  // 1. Add the dependency
  // flutter pub add google_fonts

  // 2. Define a TextTheme with a custom font
  final TextTheme appTextTheme = TextTheme(
    displayLarge: GoogleFonts.oswald(fontSize: 57, fontWeight: FontWeight.bold),
    titleLarge: GoogleFonts.roboto(fontSize: 22, fontWeight: FontWeight.w500),
    bodyMedium: GoogleFonts.openSans(fontSize: 14),
  );
  ```

### Assets and Images
* **Image Guidelines:** If images are needed, make them relevant and meaningful,
  with appropriate size, layout, and licensing (e.g., freely available). Provide
  placeholder images if real ones are not available.
* **Asset Declaration:** Declare all asset paths in your `pubspec.yaml` file.

    ```yaml
    flutter:
      uses-material-design: true
      assets:
        - assets/images/
    ```

* **Local Images:** Use `Image.asset` for local images from your asset
  bundle.

    ```dart
    Image.asset('assets/images/placeholder.png')
    ```
* **Network images:** Use NetworkImage for images loaded from the network.
* **Cached images:** For cached images, use NetworkImage a package like
  `cached_network_image`.
* **Custom Icons:** Use `ImageIcon` to display an icon from an `ImageProvider`,
  useful for custom icons not in the `Icons` class.
* **Network Images:** Use `Image.network` to display images from a URL, and
  always include `loadingBuilder` and `errorBuilder` for a better user
  experience.

    ```dart
    Image.network(
      'https://picsum.photos/200/300',
      loadingBuilder: (context, child, progress) {
        if (progress == null) return child;
        return const Center(child: CircularProgressIndicator());
      },
      errorBuilder: (context, error, stackTrace) {
        return const Icon(Icons.error);
      },
    )
    ```
## UI Theming and Styling Code

* **Responsiveness:** Use `AdaptiveLayout` located in the layout folder
  to create responsive UIs.
* **Text:** Use `Theme.of(context).textTheme` for text styles.
* **Text Fields:** Configure `textCapitalization`, `keyboardType`, and
* **Text:** Use `Theme.of(context).textTheme` for text styles.
  remote images.
* Breakpoints:** Use 'Breakpoints' with 'AdaptiveLayout' located in the 
  layout folder for designing responsive layouts for different platforms.

```dart
// When using network images, always provide an errorBuilder.
Image.network(
  'https://example.com/image.png',
  errorBuilder: (context, error, stackTrace) {
    return const Icon(Icons.error); // Show an error icon
  },
);
```

## Material Theming Best Practices

### Embrace `ThemeData` and Material 3

* **Use `ColorScheme.fromSeed()`:** Use this to generate a complete, harmonious
  color palette for both light and dark modes from a single seed color.
* **Define Light and Dark Themes:** Provide both `theme` and `darkTheme` to your
  `MaterialApp` to support system brightness settings seamlessly.
* **Centralize Component Styles:** Customize specific component themes (e.g.,
  `elevatedButtonTheme`, `cardTheme`, `appBarTheme`) within `ThemeData` to
  ensure consistency.
* **Dark/Light Mode and Theme Toggle:** Implement support for both light and
  dark themes using `theme` and `darkTheme` properties of `MaterialApp`. The
  `themeMode` property can be dynamically controlled (e.g., via a
  `ChangeNotifierProvider`) to allow for toggling between `ThemeMode.light`,
  `ThemeMode.dark`, or `ThemeMode.system`.

```dart
// main.dart
MaterialApp(
  theme: ThemeData(
    colorScheme: ColorScheme.fromSeed(
      seedColor: Colors.deepPurple,
      brightness: Brightness.light,
    ),
    textTheme: const TextTheme(
      displayLarge: TextStyle(fontSize: 57.0, fontWeight: FontWeight.bold),
      bodyMedium: TextStyle(fontSize: 14.0, height: 1.4),
    ),
  ),
  darkTheme: ThemeData(
    colorScheme: ColorScheme.fromSeed(
      seedColor: Colors.deepPurple,
      brightness: Brightness.dark,
    ),
  ),
  home: const MyHomePage(),
);
```

### Implement Design Tokens with `ThemeExtension`

For custom styles that aren't part of the standard `ThemeData`, use
`ThemeExtension` to define reusable design tokens.

* **Create a Custom Theme Extension:** Define a class that extends
  `ThemeExtension<T>` and include your custom properties.
* **Implement `copyWith` and `lerp`:** These methods are required for the
  extension to work correctly with theme transitions.
* **Register in `ThemeData`:** Add your custom extension to the `extensions`
  list in your `ThemeData`.
* **Access Tokens in Widgets:** Use `Theme.of(context).extension<MyColors>()!`
  to access your custom tokens.

```dart
// 1. Define the extension
@immutable
class MyColors extends ThemeExtension<MyColors> {
  const MyColors({required this.success, required this.danger});

  final Color? success;
  final Color? danger;

  @override
  ThemeExtension<MyColors> copyWith({Color? success, Color? danger}) {
    return MyColors(success: success ?? this.success, danger: danger ?? this.danger);
  }

  @override
  ThemeExtension<MyColors> lerp(ThemeExtension<MyColors>? other, double t) {
    if (other is! MyColors) return this;
    return MyColors(
      success: Color.lerp(success, other.success, t),
      danger: Color.lerp(danger, other.danger, t),
    );
  }
}

// 2. Register it in ThemeData
theme: ThemeData(
  extensions: const <ThemeExtension<dynamic>>[
    MyColors(success: Colors.green, danger: Colors.red),
  ],
),

// 3. Use it in a widget
Container(
  color: Theme.of(context).extension<MyColors>()!.success,
)
```

### Styling with `WidgetStateProperty`

* **`WidgetStateProperty.resolveWith`:** Provide a function that receives a
  `Set<WidgetState>` and returns the appropriate value for the current state.
* **`WidgetStateProperty.all`:** A shorthand for when the value is the same for
  all states.

```dart
// Example: Creating a button style that changes color when pressed.
final ButtonStyle myButtonStyle = ButtonStyle(
  backgroundColor: WidgetStateProperty.resolveWith<Color>(
    (Set<WidgetState> states) {
      if (states.contains(WidgetState.pressed)) {
        return Colors.green; // Color when pressed
      }
      return Colors.red; // Default color
    },
  ),
);
```

## Layout Best Practices

### Building Flexible and Overflow-Safe Layouts

#### For Rows and Columns

* **`Expanded`:** Use to make a child widget fill the remaining available space
  along the main axis.
* **`Flexible`:** Use when you want a widget to shrink to fit, but not
  necessarily grow. Don't combine `Flexible` and `Expanded` in the same `Row` or
  `Column`.
* **`Wrap`:** Use when you have a series of widgets that would overflow a `Row`
  or `Column`, and you want them to move to the next line.

#### For General Content

* **`SingleChildScrollView`:** Use when your content is intrinsically larger
  than the viewport, but is a fixed size.
* **`ListView` / `GridView`:** For long lists or grids of content, always use a
  builder constructor (`.builder`).
* **`FittedBox`:** Use to scale or fit a single child widget within its parent.
* **`LayoutBuilder`:** Use for complex, responsive layouts to make decisions
  based on the available space.

### Layering Widgets with Stack

* **`Positioned`:** Use to precisely place a child within a `Stack` by anchoring it to the edges.
* **`Align`:** Use to position a child within a `Stack` using alignments like `Alignment.center`.

### Advanced Layout with Overlays

* **`OverlayPortal`:** Use this widget to show UI elements (like custom
  dropdowns or tooltips) "on top" of everything else. It manages the
  `OverlayEntry` for you.

  ```dart
  class MyDropdown extends StatefulWidget {
    const MyDropdown({super.key});

    @override
    State<MyDropdown> createState() => _MyDropdownState();
  }

  class _MyDropdownState extends State<MyDropdown> {
    final _controller = OverlayPortalController();

    @override
    Widget build(BuildContext context) {
      return OverlayPortal(
        controller: _controller,
        overlayChildBuilder: (BuildContext context) {
          return const Positioned(
            top: 50,
            left: 10,
            child: Card(
              child: Padding(
                padding: EdgeInsets.all(8.0),
                child: Text('I am an overlay!'),
              ),
            ),
          );
        },
        child: ElevatedButton(
          onPressed: _controller.toggle,
          child: const Text('Toggle Overlay'),
        ),
      );
    }
  }
  ```

## Color Scheme Best Practices

### Contrast Ratios

* **WCAG Guidelines:** Aim to meet the Web Content Accessibility Guidelines
  (WCAG) 2.1 standards.
* **Minimum Contrast:**
    * **Normal Text:** A contrast ratio of at least **4.5:1**.
    * **Large Text:** (18pt or 14pt bold) A contrast ratio of at least **3:1**.

### Palette Selection

* **Primary, Secondary, and Accent:** Define a clear color hierarchy.
* **The 60-30-10 Rule:** A classic design rule for creating a balanced color scheme.
    * **60%** Primary/Neutral Color (Dominant)
    * **30%** Secondary Color
    * **10%** Accent Color

### Complementary Colors

* **Use with Caution:** They can be visually jarring if overused.
* **Best Use Cases:** They are excellent for accent colors to make specific
  elements pop, but generally poor for text and background pairings as they can
  cause eye strain.

### Example Palette

* **Primary:** #0D47A1 (Dark Blue)
* **Secondary:** #1976D2 (Medium Blue)
* **Accent:** #FFC107 (Amber)
* **Neutral/Text:** #212121 (Almost Black)
* **Background:** #FEFEFE (Almost White)

## Font Best Practices

### Font Selection

* **Limit Font Families:** Stick to one or two font families for the entire
  application.
* **Prioritize Legibility:** Choose fonts that are easy to read on screens of
  all sizes. Sans-serif fonts are generally preferred for UI body text.
* **System Fonts:** Consider using platform-native system fonts.
* **Google Fonts:** For a wide selection of open-source fonts, use the
  `google_fonts` package.

### Hierarchy and Scale

* **Establish a Scale:** Define a set of font sizes for different text elements
  (e.g., headlines, titles, body text, captions).
* **Use Font Weight:** Differentiate text effectively using font weights.
* **Color and Opacity:** Use color and opacity to de-emphasize less important
  text.

### Readability

* **Line Height (Leading):** Set an appropriate line height, typically **1.4x to
  1.6x** the font size.
* **Line Length:** For body text, aim for a line length of **45-75 characters**.
* **Avoid All Caps:** Do not use all caps for long-form text.

### Example Typographic Scale

```dart
// In your ThemeData
textTheme: const TextTheme(
  displayLarge: TextStyle(fontSize: 57.0, fontWeight: FontWeight.bold),
  titleLarge: TextStyle(fontSize: 22.0, fontWeight: FontWeight.bold),
  bodyLarge: TextStyle(fontSize: 16.0, height: 1.5),
  bodyMedium: TextStyle(fontSize: 14.0, height: 1.4),
  labelSmall: TextStyle(fontSize: 11.0, color: Colors.grey),
),
```

## Documentation

* **`dartdoc`:** Write `dartdoc`-style comments for all public APIs.


### Documentation Philosophy

* **Comment wisely:** Use comments to explain why the code is written a certain
  way, not what the code does. The code itself should be self-explanatory.
* **Document for the user:** Write documentation with the reader in mind. If you
  had a question and found the answer, add it to the documentation where you
  first looked. This ensures the documentation answers real-world questions.
* **No useless documentation:** If the documentation only restates the obvious
  from the code's name, it's not helpful. Good documentation provides context
  and explains what isn't immediately apparent.
* **Consistency is key:** Use consistent terminology throughout your
  documentation.

### Commenting Style

* **Use `///` for doc comments:** This allows documentation generation tools to
  pick them up.
* **Start with a single-sentence summary:** The first sentence should be a
  concise, user-centric summary ending with a period.
* **Separate the summary:** Add a blank line after the first sentence to create
  a separate paragraph. This helps tools create better summaries.
* **Avoid redundancy:** Don't repeat information that's obvious from the code's
  context, like the class name or signature.
* **Don't document both getter and setter:** For properties with both, only
  document one. The documentation tool will treat them as a single field.

### Writing Style

* **Be brief:** Write concisely.
* **Avoid jargon and acronyms:** Don't use abbreviations unless they are widely
  understood.
* **Use Markdown sparingly:** Avoid excessive markdown and never use HTML for
  formatting.
* **Use backticks for code:** Enclose code blocks in backtick fences, and
  specify the language.

### What to Document

* **Public APIs are a priority:** Always document public APIs.
* **Consider private APIs:** It's a good idea to document private APIs as well.
* **Library-level comments are helpful:** Consider adding a doc comment at the
  library level to provide a general overview.
* **Include code samples:** Where appropriate, add code samples to illustrate usage.
* **Explain parameters, return values, and exceptions:** Use prose to describe
  what a function expects, what it returns, and what errors it might throw.
* **Place doc comments before annotations:** Documentation should come before
  any metadata annotations.

## Accessibility (A11Y)
Implement accessibility features to empower all users, assuming a wide variety
of users with different physical abilities, mental abilities, age groups,
education levels, and learning styles.

* **Color Contrast:** Ensure text has a contrast ratio of at least **4.5:1**
  against its background.
* **Dynamic Text Scaling:** Test your UI to ensure it remains usable when users
  increase the system font size.
* **Semantic Labels:** Use the `Semantics` widget to provide clear, descriptive
  labels for UI elements.
* **Screen Reader Testing:** Regularly test your app with TalkBack (Android) and
  VoiceOver (iOS).

# Widget View Pattern - AI Instructions

## Overview

When creating Flutter widgets, use the **Widget View Pattern** to separate presentation logic from state management logic. This pattern improves code organization, testability, and maintainability.

## Base Classes

The widget_view package provides two abstract base classes:

### WidgetView Class

```dart
/// A base class for separating presentation logic from state logic in StatefulWidgets.
///
/// This pattern allows you to split a StatefulWidget into two parts:
/// - The StatefulWidget and State class handle state management and lifecycle
/// - The WidgetView handles the presentation (build method)
///
/// This separation improves code organization, readability, and testability.
abstract class WidgetView<
  TWidget extends StatefulWidget,
  TState extends State<TWidget>
>
    extends StatelessWidget {
  /// Creates a WidgetView with the given state.
  ///
  /// The [state] parameter must not be null and should be the state
  /// instance from the corresponding StatefulWidget.
  const WidgetView(this.state, {super.key});

  /// The state instance from the StatefulWidget.
  ///
  /// This provides access to all state variables and methods.
  final TState state;

  /// Convenience getter to access the widget from the state.
  ///
  /// This is equivalent to calling `state.widget`.
  TWidget get widget => state.widget;

  @override
  Widget build(BuildContext context);
}
```

### StatelessView Class

```dart
/// A base class for creating reusable presentation components from StatelessWidgets.
///
/// This pattern allows you to extract the build logic of a StatelessWidget
/// into a separate view class, making it easier to compose and reuse UI components.
abstract class StatelessView<TWidget extends StatelessWidget>
    extends StatelessWidget {
  /// Creates a StatelessView with the given widget.
  ///
  /// The [widget] parameter must not be null and should be the
  /// StatelessWidget instance that this view presents.
  const StatelessView(this.widget, {super.key});

  /// The StatelessWidget instance that this view presents.
  ///
  /// This provides access to all properties of the widget.
  final TWidget widget;

  @override
  Widget build(BuildContext context);
}
```

## When to Use Widget View Pattern

### Use `WidgetView` when:

1. **Creating StatefulWidgets with complex state management**
   - The widget manages internal state (counters, form data, animations, etc.)
   - You need to separate business logic from presentation logic
   - The build method is large and would benefit from being isolated

2. **Multiple view presentations based on state**
   - Different UI layouts based on state variables
   - Conditional rendering that could be organized in separate view classes
   - View logic is complex enough to warrant separation

3. **Improving testability**
   - You want to test presentation logic independently from state logic
   - You need to mock state for UI testing

### Use `StatelessView` when:

1. **Creating reusable presentation components**
   - The widget only displays data without managing state
   - You want to extract presentation logic for reuse
   - The widget receives all data through constructor parameters

2. **Multiple view presentations based on properties**
   - Different layouts based on passed variables
   - Conditional rendering based on widget properties
   - Switching between different presentations of the same data

## Implementation Guidelines

### Example 1: Basic StatefulWidget with WidgetView

**Complete working example of a counter widget:**

```dart
import 'package:flutter/material.dart';
import 'package:widget_view/widget_view.dart';

// 1. Create the StatefulWidget
class Counter extends StatefulWidget {
  const Counter({super.key, required this.initialValue});

  final int initialValue;

  @override
  State<Counter> createState() => _CounterState();
}

// 2. Create the State class (handles state and logic)
class _CounterState extends State<Counter> {
  late int _count;

  @override
  void initState() {
    super.initState();
    _count = widget.initialValue;
  }

  void increment() {
    setState(() {
      _count++;
    });
  }

  void decrement() {
    setState(() {
      _count--;
    });
  }

  void reset() {
    setState(() {
      _count = widget.initialValue;
    });
  }

  // 3. Return the view from build method
  @override
  Widget build(BuildContext context) => _CounterView(this);
}

// 4. Create the WidgetView (handles presentation)
class _CounterView extends WidgetView<Counter, _CounterState> {
  const _CounterView(_CounterState state) : super(state);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Counter Example'),
        actions: [
          IconButton(
            icon: const Icon(Icons.refresh),
            onPressed: state.reset,
          ),
        ],
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Count: ${state._count}',
              style: Theme.of(context).textTheme.headlineLarge,
            ),
            const SizedBox(height: 24),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                ElevatedButton.icon(
                  onPressed: state.decrement,
                  icon: const Icon(Icons.remove),
                  label: const Text('Decrement'),
                ),
                const SizedBox(width: 16),
                ElevatedButton.icon(
                  onPressed: state.increment,
                  icon: const Icon(Icons.add),
                  label: const Text('Increment'),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```

### Example 2: Multiple View Presentations with State Switching

**Complete working example of a widget with multiple view modes:**

```dart
import 'package:flutter/material.dart';
import 'package:widget_view/widget_view.dart';

// 1. Create the StatefulWidget
class ProductCatalog extends StatefulWidget {
  const ProductCatalog({super.key, required this.products});

  final List<Product> products;

  @override
  State<ProductCatalog> createState() => _ProductCatalogState();
}

// Helper class for product data
class Product {
  const Product({
    required this.id,
    required this.name,
    required this.price,
    required this.imageUrl,
  });

  final String id;
  final String name;
  final double price;
  final String imageUrl;
}

// 2. Create the State class
class _ProductCatalogState extends State<ProductCatalog> {
  ViewMode _currentViewMode = ViewMode.grid;

  void switchToGridView() {
    setState(() {
      _currentViewMode = ViewMode.grid;
    });
  }

  void switchToListView() {
    setState(() {
      _currentViewMode = ViewMode.list;
    });
  }

  void switchToCompactView() {
    setState(() {
      _currentViewMode = ViewMode.compact;
    });
  }

  // 3. Return different views based on state
  @override
  Widget build(BuildContext context) {
    switch (_currentViewMode) {
      case ViewMode.grid:
        return _ProductCatalogGridView(this);
      case ViewMode.list:
        return _ProductCatalogListView(this);
      case ViewMode.compact:
        return _ProductCatalogCompactView(this);
    }
  }
}

enum ViewMode { grid, list, compact }

// 4. Create the Grid view presentation
class _ProductCatalogGridView extends WidgetView<ProductCatalog, _ProductCatalogState> {
  const _ProductCatalogGridView(_ProductCatalogState state) : super(state);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Products - Grid View'),
        actions: _buildViewSwitcher(context),
      ),
      body: GridView.builder(
        padding: const EdgeInsets.all(16),
        itemCount: widget.products.length,
        gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 2,
          crossAxisSpacing: 16,
          mainAxisSpacing: 16,
          childAspectRatio: 0.75,
        ),
        itemBuilder: (context, index) {
          final product = widget.products[index];
          return Card(
            clipBehavior: Clip.antiAlias,
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Expanded(
                  child: Image.network(
                    product.imageUrl,
                    fit: BoxFit.cover,
                    width: double.infinity,
                  ),
                ),
                Padding(
                  padding: const EdgeInsets.all(8.0),
                  child: Column(
                    crossAxisAlignment: CrossAxisAlignment.start,
                    children: [
                      Text(
                        product.name,
                        style: const TextStyle(fontWeight: FontWeight.bold),
                        maxLines: 2,
                        overflow: TextOverflow.ellipsis,
                      ),
                      Text(
                        '\$${product.price.toStringAsFixed(2)}',
                        style: const TextStyle(color: Colors.green),
                      ),
                    ],
                  ),
                ),
              ],
            ),
          );
        },
      ),
    );
  }

  List<Widget> _buildViewSwitcher(BuildContext context) {
    return [
      IconButton(
        icon: const Icon(Icons.grid_view),
        onPressed: state.switchToGridView,
        color: Colors.blue,
      ),
      IconButton(
        icon: const Icon(Icons.list),
        onPressed: state.switchToListView,
      ),
      IconButton(
        icon: const Icon(Icons.view_compact),
        onPressed: state.switchToCompactView,
      ),
    ];
  }
}

// 5. Create the List view presentation
class _ProductCatalogListView extends WidgetView<ProductCatalog, _ProductCatalogState> {
  const _ProductCatalogListView(_ProductCatalogState state) : super(state);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Products - List View'),
        actions: _buildViewSwitcher(context),
      ),
      body: ListView.builder(
        itemCount: widget.products.length,
        itemBuilder: (context, index) {
          final product = widget.products[index];
          return Card(
            margin: const EdgeInsets.symmetric(horizontal: 16, vertical: 8),
            child: ListTile(
              leading: ClipRRect(
                borderRadius: BorderRadius.circular(8),
                child: Image.network(
                  product.imageUrl,
                  width: 60,
                  height: 60,
                  fit: BoxFit.cover,
                ),
              ),
              title: Text(product.name),
              subtitle: Text('\$${product.price.toStringAsFixed(2)}'),
              trailing: const Icon(Icons.arrow_forward_ios),
            ),
          );
        },
      ),
    );
  }

  List<Widget> _buildViewSwitcher(BuildContext context) {
    return [
      IconButton(
        icon: const Icon(Icons.grid_view),
        onPressed: state.switchToGridView,
      ),
      IconButton(
        icon: const Icon(Icons.list),
        onPressed: state.switchToListView,
        color: Colors.blue,
      ),
      IconButton(
        icon: const Icon(Icons.view_compact),
        onPressed: state.switchToCompactView,
      ),
    ];
  }
}

// 6. Create the Compact view presentation
class _ProductCatalogCompactView extends WidgetView<ProductCatalog, _ProductCatalogState> {
  const _ProductCatalogCompactView(_ProductCatalogState state) : super(state);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Products - Compact View'),
        actions: _buildViewSwitcher(context),
      ),
      body: ListView.builder(
        itemCount: widget.products.length,
        itemBuilder: (context, index) {
          final product = widget.products[index];
          return ListTile(
            dense: true,
            title: Text(product.name),
            trailing: Text(
              '\$${product.price.toStringAsFixed(2)}',
              style: const TextStyle(
                fontWeight: FontWeight.bold,
                color: Colors.green,
              ),
            ),
          );
        },
      ),
    );
  }

  List<Widget> _buildViewSwitcher(BuildContext context) {
    return [
      IconButton(
        icon: const Icon(Icons.grid_view),
        onPressed: state.switchToGridView,
      ),
      IconButton(
        icon: const Icon(Icons.list),
        onPressed: state.switchToListView,
      ),
      IconButton(
        icon: const Icon(Icons.view_compact),
        onPressed: state.switchToCompactView,
        color: Colors.blue,
      ),
    ];
  }
}
```

### Example 3: StatelessWidget with Multiple StatelessView Presentations

**Complete working example of a user profile widget with responsive layouts:**

```dart
import 'package:flutter/material.dart';
import 'package:widget_view/widget_view.dart';

// 1. Create the StatelessWidget
class UserProfile extends StatelessWidget {
  const UserProfile({
    super.key,
    required this.user,
    this.displayMode = DisplayMode.card,
  });

  final User user;
  final DisplayMode displayMode;

  // 2. Return different views based on properties
  @override
  Widget build(BuildContext context) {
    switch (displayMode) {
      case DisplayMode.card:
        return _UserProfileCardView(this);
      case DisplayMode.list:
        return _UserProfileListView(this);
      case DisplayMode.compact:
        return _UserProfileCompactView(this);
    }
  }
}

// Helper classes
class User {
  const User({
    required this.id,
    required this.name,
    required this.email,
    required this.avatarUrl,
    required this.bio,
    required this.role,
  });

  final String id;
  final String name;
  final String email;
  final String avatarUrl;
  final String bio;
  final String role;
}

enum DisplayMode { card, list, compact }

// 3. Create the Card view presentation
class _UserProfileCardView extends StatelessView<UserProfile> {
  const _UserProfileCardView(UserProfile widget) : super(widget);

  @override
  Widget build(BuildContext context) {
    return Card(
      elevation: 4,
      margin: const EdgeInsets.all(16),
      child: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Row(
              children: [
                CircleAvatar(
                  radius: 40,
                  backgroundImage: NetworkImage(widget.user.avatarUrl),
                ),
                const SizedBox(width: 16),
                Expanded(
                  child: Column(
                    crossAxisAlignment: CrossAxisAlignment.start,
                    children: [
                      Text(
                        widget.user.name,
                        style: Theme.of(context).textTheme.headlineSmall,
                      ),
                      const SizedBox(height: 4),
                      Text(
                        widget.user.role,
                        style: Theme.of(context).textTheme.bodySmall?.copyWith(
                              color: Colors.grey[600],
                            ),
                      ),
                    ],
                  ),
                ),
              ],
            ),
            const SizedBox(height: 16),
            Text(
              widget.user.bio,
              style: Theme.of(context).textTheme.bodyMedium,
            ),
            const SizedBox(height: 12),
            Row(
              children: [
                const Icon(Icons.email, size: 16, color: Colors.grey),
                const SizedBox(width: 8),
                Text(
                  widget.user.email,
                  style: Theme.of(context).textTheme.bodySmall,
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}

// 4. Create the List view presentation
class _UserProfileListView extends StatelessView<UserProfile> {
  const _UserProfileListView(UserProfile widget) : super(widget);

  @override
  Widget build(BuildContext context) {
    return ListTile(
      leading: CircleAvatar(
        backgroundImage: NetworkImage(widget.user.avatarUrl),
      ),
      title: Text(widget.user.name),
      subtitle: Text(widget.user.email),
      trailing: Chip(
        label: Text(widget.user.role),
        backgroundColor: Colors.blue[100],
      ),
      onTap: () {
        // Handle tap
      },
    );
  }
}

// 5. Create the Compact view presentation
class _UserProfileCompactView extends StatelessView<UserProfile> {
  const _UserProfileCompactView(UserProfile widget) : super(widget);

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.symmetric(horizontal: 16, vertical: 8),
      child: Row(
        children: [
          CircleAvatar(
            radius: 20,
            backgroundImage: NetworkImage(widget.user.avatarUrl),
          ),
          const SizedBox(width: 12),
          Expanded(
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text(
                  widget.user.name,
                  style: const TextStyle(fontWeight: FontWeight.bold),
                ),
                Text(
                  widget.user.role,
                  style: TextStyle(
                    fontSize: 12,
                    color: Colors.grey[600],
                  ),
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }
}

// Example usage:
class UserListExample extends StatelessWidget {
  const UserListExample({super.key});

  @override
  Widget build(BuildContext context) {
    final users = [
      const User(
        id: '1',
        name: 'John Doe',
        email: 'john@example.com',
        avatarUrl: 'https://i.pravatar.cc/150?img=1',
        bio: 'Software engineer passionate about Flutter',
        role: 'Developer',
      ),
      // ... more users
    ];

    return Scaffold(
      appBar: AppBar(title: const Text('User Profiles')),
      body: ListView(
        children: [
          // Card view
          UserProfile(user: users[0], displayMode: DisplayMode.card),

          // List view
          UserProfile(user: users[0], displayMode: DisplayMode.list),

          // Compact view
          UserProfile(user: users[0], displayMode: DisplayMode.compact),
        ],
      ),
    );
  }
}
```

### Example 4: Form with State Management and Validation

**Complete working example showing state management with complex business logic:**

```dart
import 'package:flutter/material.dart';
import 'package:widget_view/widget_view.dart';

// 1. Create the StatefulWidget
class LoginForm extends StatefulWidget {
  const LoginForm({super.key, required this.onLogin});

  final Future<bool> Function(String email, String password) onLogin;

  @override
  State<LoginForm> createState() => _LoginFormState();
}

// 2. Create the State class with business logic
class _LoginFormState extends State<LoginForm> {
  final _formKey = GlobalKey<FormState>();
  final _emailController = TextEditingController();
  final _passwordController = TextEditingController();

  bool _isLoading = false;
  bool _obscurePassword = true;
  String? _errorMessage;

  @override
  void dispose() {
    _emailController.dispose();
    _passwordController.dispose();
    super.dispose();
  }

  void togglePasswordVisibility() {
    setState(() {
      _obscurePassword = !_obscurePassword;
    });
  }

  String? validateEmail(String? value) {
    if (value == null || value.isEmpty) {
      return 'Please enter your email';
    }
    final emailRegex = RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$');
    if (!emailRegex.hasMatch(value)) {
      return 'Please enter a valid email';
    }
    return null;
  }

  String? validatePassword(String? value) {
    if (value == null || value.isEmpty) {
      return 'Please enter your password';
    }
    if (value.length < 6) {
      return 'Password must be at least 6 characters';
    }
    return null;
  }

  Future<void> handleSubmit() async {
    setState(() {
      _errorMessage = null;
    });

    if (!_formKey.currentState!.validate()) {
      return;
    }

    setState(() {
      _isLoading = true;
    });

    try {
      final success = await widget.onLogin(
        _emailController.text,
        _passwordController.text,
      );

      if (!mounted) return;

      if (!success) {
        setState(() {
          _errorMessage = 'Invalid email or password';
          _isLoading = false;
        });
      }
    } catch (e) {
      if (!mounted) return;

      setState(() {
        _errorMessage = 'An error occurred. Please try again.';
        _isLoading = false;
      });
    }
  }

  // 3. Return the view
  @override
  Widget build(BuildContext context) => _LoginFormView(this);
}

// 4. Create the WidgetView for presentation
class _LoginFormView extends WidgetView<LoginForm, _LoginFormState> {
  const _LoginFormView(_LoginFormState state) : super(state);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Login'),
      ),
      body: SafeArea(
        child: Padding(
          padding: const EdgeInsets.all(24.0),
          child: Form(
            key: state._formKey,
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              crossAxisAlignment: CrossAxisAlignment.stretch,
              children: [
                // Logo or title
                Icon(
                  Icons.lock_outline,
                  size: 80,
                  color: Theme.of(context).primaryColor,
                ),
                const SizedBox(height: 48),

                // Email field
                TextFormField(
                  controller: state._emailController,
                  enabled: !state._isLoading,
                  keyboardType: TextInputType.emailAddress,
                  textInputAction: TextInputAction.next,
                  decoration: const InputDecoration(
                    labelText: 'Email',
                    prefixIcon: Icon(Icons.email_outlined),
                    border: OutlineInputBorder(),
                  ),
                  validator: state.validateEmail,
                ),
                const SizedBox(height: 16),

                // Password field
                TextFormField(
                  controller: state._passwordController,
                  enabled: !state._isLoading,
                  obscureText: state._obscurePassword,
                  textInputAction: TextInputAction.done,
                  decoration: InputDecoration(
                    labelText: 'Password',
                    prefixIcon: const Icon(Icons.lock_outlined),
                    suffixIcon: IconButton(
                      icon: Icon(
                        state._obscurePassword
                            ? Icons.visibility_outlined
                            : Icons.visibility_off_outlined,
                      ),
                      onPressed: state.togglePasswordVisibility,
                    ),
                    border: const OutlineInputBorder(),
                  ),
                  validator: state.validatePassword,
                  onFieldSubmitted: (_) {
                    if (!state._isLoading) {
                      state.handleSubmit();
                    }
                  },
                ),
                const SizedBox(height: 24),

                // Error message
                if (state._errorMessage != null)
                  Container(
                    padding: const EdgeInsets.all(12),
                    decoration: BoxDecoration(
                      color: Colors.red[50],
                      borderRadius: BorderRadius.circular(8),
                      border: Border.all(color: Colors.red[300]!),
                    ),
                    child: Row(
                      children: [
                        Icon(Icons.error_outline, color: Colors.red[700]),
                        const SizedBox(width: 12),
                        Expanded(
                          child: Text(
                            state._errorMessage!,
                            style: TextStyle(color: Colors.red[700]),
                          ),
                        ),
                      ],
                    ),
                  ),
                if (state._errorMessage != null) const SizedBox(height: 24),

                // Submit button
                ElevatedButton(
                  onPressed: state._isLoading ? null : state.handleSubmit,
                  style: ElevatedButton.styleFrom(
                    padding: const EdgeInsets.symmetric(vertical: 16),
                  ),
                  child: state._isLoading
                      ? const SizedBox(
                          height: 20,
                          width: 20,
                          child: CircularProgressIndicator(
                            strokeWidth: 2,
                          ),
                        )
                      : const Text(
                          'Login',
                          style: TextStyle(fontSize: 16),
                        ),
                ),
                const SizedBox(height: 16),

                // Forgot password link
                TextButton(
                  onPressed: state._isLoading ? null : () {
                    // Handle forgot password
                  },
                  child: const Text('Forgot password?'),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}

// Example usage:
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: LoginForm(
        onLogin: (email, password) async {
          // Simulate API call
          await Future.delayed(const Duration(seconds: 2));

          // Mock authentication logic
          return email == 'test@example.com' && password == 'password123';
        },
      ),
    );
  }
}
```

## Key Rules to Follow

1. **Always make view classes private** (prefix with `_`)
   - Views are implementation details and should not be exposed

2. **Use const constructors**
   - Both the view classes and their constructors should be const when possible
   - This enables Flutter's widget optimization

3. **Access state/widget through the provided properties**
   - In `WidgetView`: use `state` to access state variables and methods
   - In `WidgetView`: use `widget` (or `state.widget`) to access widget properties
   - In `StatelessView`: use `widget` to access widget properties

4. **Keep business logic in the State class**
   - State management, API calls, and business logic belong in the State class
   - The view should only handle presentation and call state methods

5. **Name views descriptively**
   - Use pattern: `_{WidgetName}View` for single views
   - Use pattern: `_{WidgetName}{Variant}View` for multiple views (e.g., `_UserCardCompactView`)

6. **Return the view from the build method**
   - The State/StatelessWidget's build method should instantiate and return the view
   - Switch between views based on state variables or widget properties

## Benefits of This Pattern

- **Separation of Concerns**: State logic and presentation logic are clearly separated
- **Improved Readability**: Smaller, focused classes are easier to understand
- **Better Testability**: Views can be tested independently from state logic
- **Easier Maintenance**: Changes to presentation don't affect state management
- **Reusability**: Multiple views can share the same state logic
- **Flexibility**: Easy to switch between different presentations based on state or properties

## When NOT to Use

- Simple widgets with minimal logic (< 20 lines in build method)
- Widgets that are already simple and don't manage state
- One-off widgets that won't benefit from the separation
- When the added abstraction doesn't provide clear value

## Example Decision Tree

```
Does the widget manage state?
├─ Yes → Use WidgetView pattern
│  └─ Does it need multiple view presentations?
│     ├─ Yes → Create multiple WidgetView classes, switch in State.build()
│     └─ No → Create single WidgetView class
│
└─ No → Is it a StatelessWidget?
   └─ Yes → Does it need multiple view presentations or have complex build logic?
      ├─ Yes → Use StatelessView pattern with multiple views
      └─ No → Regular StatelessWidget is fine
```

## Import Statement

Always import the widget_view package:

```dart
import 'package:widget_view/widget_view.dart';
```

## Quick Reference Template

### StatefulWidget with WidgetView Template

```dart
import 'package:flutter/material.dart';
import 'package:widget_view/widget_view.dart';

class MyWidget extends StatefulWidget {
  const MyWidget({super.key});

  @override
  State<MyWidget> createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  // State variables here

  // Business logic methods here

  @override
  Widget build(BuildContext context) => _MyWidgetView(this);
}

class _MyWidgetView extends WidgetView<MyWidget, _MyWidgetState> {
  const _MyWidgetView(_MyWidgetState state) : super(state);

  @override
  Widget build(BuildContext context) {
    // UI code here - access state via state.variableName
    return Container();
  }
}
```

### StatelessWidget with StatelessView Template

```dart
import 'package:flutter/material.dart';
import 'package:widget_view/widget_view.dart';

class MyWidget extends StatelessWidget {
  const MyWidget({super.key});

  @override
  Widget build(BuildContext context) => _MyWidgetView(this);
}

class _MyWidgetView extends StatelessView<MyWidget> {
  const _MyWidgetView(MyWidget widget) : super(widget);

  @override
  Widget build(BuildContext context) {
    // UI code here - access properties via widget.propertyName
    return Container();
  }
}
```

### Multiple Views with State Switching Template

```dart
import 'package:flutter/material.dart';
import 'package:widget_view/widget_view.dart';

enum ViewMode { mode1, mode2 }

class MyWidget extends StatefulWidget {
  const MyWidget({super.key});

  @override
  State<MyWidget> createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  ViewMode _currentMode = ViewMode.mode1;

  void switchMode(ViewMode mode) {
    setState(() {
      _currentMode = mode;
    });
  }

  @override
  Widget build(BuildContext context) {
    switch (_currentMode) {
      case ViewMode.mode1:
        return _MyWidgetMode1View(this);
      case ViewMode.mode2:
        return _MyWidgetMode2View(this);
    }
  }
}

class _MyWidgetMode1View extends WidgetView<MyWidget, _MyWidgetState> {
  const _MyWidgetMode1View(_MyWidgetState state) : super(state);

  @override
  Widget build(BuildContext context) {
    return Container(); // First view implementation
  }
}

class _MyWidgetMode2View extends WidgetView<MyWidget, _MyWidgetState> {
  const _MyWidgetMode2View(_MyWidgetState state) : super(state);

  @override
  Widget build(BuildContext context) {
    return Container(); // Second view implementation
  }
}
```

## Summary for AI Consumption

**When you encounter these patterns in user requests:**

1. **"Create a widget that manages state"** → Use WidgetView pattern
2. **"Add multiple view modes/presentations"** → Create multiple view classes with switching logic
3. **"Separate business logic from UI"** → State handles logic, View handles UI
4. **"Make this widget testable"** → Apply WidgetView pattern for separation
5. **"Create different layouts based on..."** → Multiple views with conditional rendering

**Key implementation steps:**
1. Create the widget class (StatefulWidget or StatelessWidget)
2. Create the state class with all logic (if stateful)
3. Return appropriate view from build method
4. Create private view class(es) extending WidgetView/StatelessView
5. Implement presentation logic in view's build method
6. Access state/widget properties through provided getters

**Always remember:**
- View classes are private (prefix with `_`)
- State class handles business logic and state management
- View classes only handle presentation
- Use `state.propertyName` in WidgetView to access state
- Use `widget.propertyName` in StatelessView to access widget properties
- Multiple views can share the same state
- Switch between views based on state variables or widget properties
