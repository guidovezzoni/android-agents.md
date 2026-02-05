# Android

## Architecture
- **MVVM Architecture**: Use Model-View-ViewModel pattern
- **Clean Architecture**: When required use a clean architecture approach, separating data, domain, and UI.
- **Dependency Injection**: Use Hilt for DI (when needed)
- **Async Operations**: Use Coroutines and Flow for asynchronous operations

## Jetpack Compose
- **Composable Structure:**
    - Parameters usually include a `Modifier` as the first optional argument: `modifier: Modifier = Modifier`.
    - Avoid hardcoded dimensions; use `dimens.xml` or constant values.
- **State Hoisting**: Keep composables stateless, hoist state to caller or ViewModel
- **Composable Previews**: Always create a preview for the stateless composable, considering all the reasonable states that the composable could have.
  - The preview should be named `Preview[ComponentName]`.
  - It should be `private`.
  - It must be wrapped in the application's main theme (e.g., `MyAppTheme { ... }`).
  - Set `showBackground = true` in the `@Preview` annotation.

- Use `mutableStateOf` only for state that needs to trigger recomposition
- Use `rememberSaveable` for state that should survive configuration changes
- **Material 3:** Always use Material 3 components unless specified otherwise.
- **Scaffold Usage:** When creating screens, start with a `Scaffold` to handle top bars, floating action buttons, and snackbars correctly.

## Legacy Code
- Do not use `findViewById`; strictly use Jetpack Compose or ViewBinding (if working with legacy views).

## Multi-language
- Base language should always be English
- When adding a new user facing string, always extract it in the strings.xml file for easy translation
- Common strings, like button names, should be listed at the top of strings.xml and have this prefix: "global_"
- When a new string is added or modified to strings.xml, update the same value in other languages that might be present, translating it accordingly.
- **Ellipsis**: Always replace three dots with ellipsis

## Development Best Practices
- **Literals extraction**: When adding new code or modifying existing code always extract literals in private constants to be held in the same class/file in which they are used. By literals I mean:
  - strings and numeric
  - non UI/user facing, only development related
- **Immutability**: Always prefer `val` over `var` for immutable properties
- **EOF Empty Line**: Always leave an empty line at the end of the source file.

## Testing Guidelines

### Unit Tests
- Located in `app/src/test/`
- Use JUnit 4
- Test composables with `compose-ui-test` library
- using the GIVEN / WHEN / THEN pattern
- Mock dependencies appropriately using MockK
- Create a setup method if required
- use runTest if required
- use UnconfinedTestDispatcher if required
- use @MockK notation if required
- extract in a variable the expected value before asserting
- cover all reasonable cases, but keeps the coverage over 80%


### Instrumentation Tests
- Located in `app/src/androidTest/`
- Use AndroidX Test and Espresso
- Test UI interactions and integration scenarios
