# MVVMate

MVVMate is a minimal state management library for Compose Multiplatform, based on the MVVM architecture.

[![Maven Central](https://img.shields.io/maven-central/v/com.helloanwar.mvvmate.core)](https://search.maven.org/artifact/com.helloanwar/mvvmate.core)
[![Documentation](https://img.shields.io/badge/docs-API-blue)](https://anwarpro.github.io/mvvmate)

## Overview

This library provides base classes and interfaces for managing UI state, handling user actions, and emitting side effects in a Compose Multiplatform project.

### Key Components

- **BaseViewModel**: A base ViewModel class that manages state and handles user actions.
- **BaseViewModelWithEffect**: Extends `BaseViewModel` to also manage UI side effects.
- **UiState**: A marker interface for defining UI states.
- **UiAction**: A marker interface for user actions.
- **UiEffect**: A marker interface for UI side effects.

## Installation

To use MVVMate in your project, add the following to your `build.gradle.kts`:

### For Kotlin Multiplatform Projects:

```kotlin
kotlin {
    sourceSets {
        val commonMain by getting {
            dependencies {
                implementation("com.helloanwar.mvvmate.core:1.0.0")
            }
        }
    }
}
```

### For Android Projects:

```kotlin
dependencies {
    implementation("com.helloanwar.mvvmate.core:1.0.0")
}
```

## Usage

Here's a simple example of how you can use `MVVMate` in your Compose Multiplatform project:

```kotlin
// Define your UI State
data class MyUiState(val message: String = "") : UiState

// Define your User Actions
sealed class MyUiAction : UiAction {
    object ShowMessage : MyUiAction()
}

// Define your ViewModel
class MyViewModel : BaseViewModel<MyUiState, MyUiAction>(MyUiState()) {
    override suspend fun onAction(action: MyUiAction) {
        when (action) {
            MyUiAction.ShowMessage -> updateState { copy(message = "Hello, World!") }
        }
    }
}

// Use the ViewModel in your Composable function
@Composable
fun MyScreen(viewModel: MyViewModel) {
    val state by viewModel.state.collectAsState()

    Text(text = state.message)
    Button(onClick = { viewModel.handleAction(MyUiAction.ShowMessage) }) {
        Text("Show Message")
    }
}
```

## API Documentation

For more detailed information, you can check the [API documentation](https://anwarpro.github.io/mvvmate) generated by Dokka.
