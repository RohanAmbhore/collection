<a href="https://code.visualstudio.com/updates/v1_13#_merge-conflict-coloring-and-actions">https://code.visualstudio.com/updates/v1_13#_merge-conflict-coloring-and-actions</a><div id="articleHeader"><h1>May 2017 (version 1.13)</h1></div>
<p><strong>Update 1.13.1</strong>: The update addresses these <a href="https://github.com/Microsoft/vscode/milestone/45?closed=1" target="_blank">issues</a>.</p>
<p>Downloads: <a href="https://vscode-update.azurewebsites.net/1.13.1/win32/stable" target="_blank">Windows</a> | <a href="https://vscode-update.azurewebsites.net/1.13.1/darwin/stable" target="_blank">Mac</a> | Linux 64-bit: <a href="https://vscode-update.azurewebsites.net/1.13.1/linux-x64/stable" target="_blank">.tar.gz</a> <a href="https://vscode-update.azurewebsites.net/1.13.1/linux-deb-x64/stable" target="_blank">.deb</a> <a href="https://vscode-update.azurewebsites.net/1.13.1/linux-rpm-x64/stable" target="_blank">.rpm</a> | Linux 32-bit: <a href="https://vscode-update.azurewebsites.net/1.13.1/linux-ia32/stable" target="_blank">.tar.gz</a> <a href="https://vscode-update.azurewebsites.net/1.13.1/linux-deb-ia32/stable" target="_blank">.deb</a> <a href="https://vscode-update.azurewebsites.net/1.13.1/linux-rpm-ia32/stable" target="_blank">.rpm</a></p>
<hr />
<p>Welcome to the May 2017 release of Visual Studio Code. There are a number of significant updates in this version that we hope you will like, some of the key highlights include:</p>
<ul>
<li><strong><a href="#_changed-setting-defaults" target="_blank">Changes to settings defaults</a></strong> - Enabled by default: extensions auto-update, editor drag and drop, and minimap (outline view).</li>
<li><strong><a href="#_add-multiple-cursors-with-ctrl-cmd-click" target="_blank">Set multiple cursors with Ctrl/Cmd + Click</a></strong> - Add multi-cursors just like Sublime Text and Atom.</li>
<li><strong><a href="#_merge-conflict-coloring-and-actions" target="_blank">Improved Git merge</a></strong> - Inline merge actions with Accept Changes CodeLens.</li>
<li><strong><a href="#_suggestion-list-and-documentation-side-by-side" target="_blank">Better IntelliSense details</a></strong> - Easily toggle full suggestion documentation.</li>
<li><strong><a href="#_emmet-abbreviation-expansion-in-suggestion-list" target="_blank">Emmet abbreviations display</a></strong> - Preview Emmet expansions as you type.</li>
<li><strong><a href="#_multi-cursor-snippets" target="_blank">Enhanced snippets</a></strong> - Increase your productivity with multi-cursor and nested snippets.</li>
<li><strong><a href="#_improved-stepping-performance" target="_blank">Faster debugger performance</a></strong> - Stepping through source code is significantly faster.</li>
<li><strong><a href="#_file-link-detection-in-exception-peek-ui" target="_blank">File links in exception stack traces</a></strong> - Jump directly to source code from exception stack traces.</li>
<li><strong><a href="#_recipes-for-nonstandard-debugging-scenarios" target="_blank">Docker and MERN debugging recipes</a></strong> - Debug configuration examples for Docker and MERN stack projects.</li>
<li><strong><a href="#_new-theming-colors" target="_blank">More workbench theming colors</a></strong> - We've added more VS Code customizable colors.</li>
<li><strong><a href="#_better-nvda-support" target="_blank">Better NVDA support</a></strong> - Accessibility improvements for the NVDA screen reader.</li>
</ul>
<blockquote>
<p>If you'd like to read these release notes online, you can go to <a href="https://code.visualstudio.com/updates" target="_blank">Updates</a> on <a href="https://code.visualstudio.com" target="_blank">code.visualstudio.com</a>.</p>
</blockquote>
<p>The release notes are arranged in the following sections related to VS Code focus areas. Here are some further updates:</p>
<ul>
<li><strong><a href="#_workbench" target="_blank">Workbench</a></strong> - Filenames in symbol search, disable menu bar mnemonics.</li>
<li><strong><a href="#_editor" target="_blank">Editor</a></strong> - Resizable Find widget, new folding control settings.</li>
<li><strong><a href="#_languages" target="_blank">Languages</a></strong> - JSX/TSX component highlighting, Markdown headers in symbol search.</li>
<li><strong><a href="#_debugging" target="_blank">Debugging</a></strong> - Copy All from Debug Console, local/remote paths in launch configurations.</li>
<li><strong><a href="#_tasks" target="_blank">Tasks</a></strong> - Auto-detect and customize Gulp and Grunt tasks to run in VS Code.</li>
<li><strong><a href="#_extension-authoring" target="_blank">Extension Authoring</a></strong> - Custom views in the Explorer, reference theme colors.</li>
</ul>
<p><strong>Insiders:</strong> Want to see new features as soon as possible? You can download the nightly <a href="https://code.visualstudio.com/insiders" target="_blank">Insiders</a> build and try the latest updates as soon as they are available.</p>
<h2 id="_setting-changes">Setting changes<a href="#_setting-changes" target="_blank">#</a></h2>
<h3 id="_changed-setting-defaults">Changed setting defaults<a href="#_changed-setting-defaults" target="_blank">#</a></h3>
<p>One thing you may notice right away in the May release is that we've changed the default value of several settings. Features such as minimap (outline view), icon themes, and indent guides have been off by default and we think they are so useful, we want to showcase them.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/new-setting-defaults.png" alt="new setting defaults" /></div></p>
<p>Here are the new default settings:</p>
<table>
<thead>
<tr>
<th>Setting</th>
<th>New Default</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>editor.minimap.enabled</code></td>
<td>true</td>
<td>Show file minimap (outline view) in the right gutter</td>
</tr>
<tr>
<td><code>workbench.iconTheme</code></td>
<td>"vs-seti"</td>
<td>Use <code>vs-seti</code> file icon theme</td>
</tr>
<tr>
<td><code>editor.renderIndentGuides</code></td>
<td>true</td>
<td>Display editor indentation guides</td>
</tr>
<tr>
<td><code>editor.dragAndDrop</code></td>
<td>true</td>
<td>Move editor selections with drag and drop</td>
</tr>
<tr>
<td><code>extensions.autoUpdate</code></td>
<td>true</td>
<td>Automatically update extensions</td>
</tr>
<tr>
<td><code>window.openFilesInNewWindow</code></td>
<td>"off"</td>
<td>Open files in the running VS Code instance</td>
</tr>
</tbody>
</table>
<p>Of course, you can still configure VS Code to your preference with user or workspace <a href="https://code.visualstudio.com/docs/getstarted/settings" target="_blank">settings</a> (<strong>File</strong> &gt; <strong>Preferences</strong> &gt; <strong>Settings</strong> or keyboard shortcut ⌘,).</p>
<h3 id="_add-multiple-cursors-with-ctrl-cmd-click">Add multiple cursors with Ctrl / Cmd + Click<a href="#_add-multiple-cursors-with-ctrl-cmd-click" target="_blank">#</a></h3>
<p>We have introduced a new setting, <code>editor.multiCursorModifier</code>, to change the modifier key for applying multiple cursors to <code>Cmd+Click</code> on macOS and <code>Ctrl+Click</code> on Windows and Linux. This lets users coming from other editors such as Sublime Text or Atom continue to use the keyboard modifier they are familiar with.</p>
<p>The setting can be set to:</p>
<ul>
<li><code>ctrlCmd</code> - Maps to <code>Ctrl</code> on Windows and <code>Cmd</code> on macOS.</li>
<li><code>alt</code> - The existing default <code>Alt</code>.</li>
</ul>
<p>There's also a new menu item <strong>Use Ctrl+Click for Multi-Cursor</strong> in the <strong>Selection</strong> menu to quickly toggle this setting.</p>
<p>The <strong>Go To Definition</strong> and <strong>Open Link</strong> gestures will also respect this setting and adapt such that they do not conflict. For example, when the setting is <code>ctrlCmd</code>, multiple cursors can be added with <code>Ctrl/Cmd+Click</code>, and opening links or going to definition can be invoked with <code>Alt+Click</code>.</p>
<p>With fixing <a href="https://github.com/Microsoft/vscode/issues/2106" target="_blank">Issue #2106</a>, it is now possible to also remove a cursor by using the same gesture on top of an existing selection.</p>
<h2 id="_workbench">Workbench<a href="#_workbench" target="_blank">#</a></h2>
<h3 id="_filenames-in-symbol-search-results">Filenames in symbol search results<a href="#_filenames-in-symbol-search-results" target="_blank">#</a></h3>
<p>You can use workspace symbol search (⌘T) to quickly find symbols in your workspace. The list of results now includes the filename of each symbol:</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/typescript-workspace-symbol-names.png" alt="symbol search includes filename" /></div></p>
<h3 id="_disable-menu-bar-mnemonics">Disable menu bar mnemonics<a href="#_disable-menu-bar-mnemonics" target="_blank">#</a></h3>
<p>A new setting <code>window.enableMenuBarMnemonics</code> was added to disable all mnemonics (hot keys) in the menu bar (on Windows and Linux). This frees up some <code>Alt+</code> keyboard shortcuts to bind to other commands.</p>
<h3 id="_install-additional-scm-providers">Install Additional SCM Providers<a href="#_install-additional-scm-providers" target="_blank">#</a></h3>
<p>We have introduced a new command <strong>Install Additional SCM Providers...</strong> to make it easier to discover and install SCM providers from the VS Code Marketplace. The command is available under the <strong>Switch SCM Provider...</strong> command in the <strong>Source Control</strong> view and <strong>SCM: Switch SCM Provider</strong> in the <strong>Command Palette</strong>.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/additional-scm-providers.png" alt="Install Additional SCM Providers" /></div></p>
<h3 id="_go-to-implementation-and-go-to-type-definition-added-to-the-go-menu">Go to Implementation and Go to Type Definition added to the Go menu<a href="#_go-to-implementation-and-go-to-type-definition-added-to-the-go-menu" target="_blank">#</a></h3>
<p>The <strong>Go</strong> menu now includes the <strong>Go to Implementation</strong> and <strong>Go to Type Definition</strong> commands:</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/go-menu.png" alt="New Go menu items" /></div></p>
<h3 id="_preserving-view-state-for-resource-editors">Preserving view state for resource editors<a href="#_preserving-view-state-for-resource-editors" target="_blank">#</a></h3>
<p>We are now preserving the view state for resource editors when you switch between them. This comes in handy when debugging internal modules since we now preserve the scroll position and all other view data for internal module editors. However, we always clear the view state when a user closes the editor.</p>
<h3 id="_high-contrast-theme">High Contrast theme<a href="#_high-contrast-theme" target="_blank">#</a></h3>
<p>We have improved the High Contrast theme to include more token colors and to use selection and Status Bar colors for clearer contrast.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/high-contrast.png" alt="High Contrast theme improvements" /></div></p>
<h3 id="_new-theming-colors">New theming colors<a href="#_new-theming-colors" target="_blank">#</a></h3>
<p>We received a lot of feedback for our workbench theming support and are happy to see more and more themes adopting the workbench colors! During this milestone, we added almost 50 new colors as well as did some tweaks to existing colors. These colors can be set by themes or directly by the user with the <code>workbench.colorCustomizations</code> setting.</p>
<p>You can review the new colors in the updated <a href="https://code.visualstudio.com/docs/getstarted/theme-color-reference" target="_blank">Theme Color Reference</a>.</p>
<p>Below are the existing color behavior changes:</p>
<table>
<thead>
<tr>
<th>Key</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>panel.border</code></td>
<td>Now overwrites the value of <code>contrastBorder</code>, allowing a more specific color if <code>contrastBorder</code> is set.</td>
</tr>
<tr>
<td><code>tab.border</code></td>
<td>Now overwrites the value of <code>contrastBorder</code>, allowing a more specific color if <code>contrastBorder</code> is set.</td>
</tr>
<tr>
<td><code>editorGroup.border</code></td>
<td>Now overwrites the value of <code>contrastBorder</code>, allowing a more specific color if <code>contrastBorder</code> is set.</td>
</tr>
<tr>
<td><code>list.*</code></td>
<td>All list colors can now be set even in the presence of <code>contrastBorder</code> and <code>contrastActiveBorder</code>.</td>
</tr>
</tbody>
</table>
<h3 id="_multiroot-workspaces">Multi-root workspaces<a href="#_multiroot-workspaces" target="_blank">#</a></h3>
<p>During this milestone, we made some significant steps towards supporting multi-root (multiple project folder) workspaces in VS Code. In case you are wondering why it is taking us a little bit longer to tackle this feature request, please read <a href="https://github.com/Microsoft/vscode/issues/396#issuecomment-301842430" target="_blank">Daniel's excellent explanation</a>.</p>
<p>We focused on UX and sketched up how we could provide this feature with our current architecture without introducing too many new concepts. After sharing the designs with the engineering team, we ran 2 user studies to validate our assumptions. We encourage you to watch the recordings of these studies if you are interested and provide feedback:</p>

<p>With the UX work behind us, we feel that we can finally start implementing this feature request. Thanks for your patience!</p>
<h2 id="_editor">Editor<a href="#_editor" target="_blank">#</a></h2>
<h3 id="_merge-conflict-coloring-and-actions">Merge conflict coloring and actions<a href="#_merge-conflict-coloring-and-actions" target="_blank">#</a></h3>
<p>Inline merge conflicts are now colored and come with actions to accept either or both of the changes. Previously available as the popular Better Merge extension, this functionality is now built-in. Thanks to <a href="https://github.com/pprice" target="_blank">Phil Price (@pprice)</a>, the author of Better Merge, for the PR.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/merge-conflict.png" alt="markdown symbols with header level" /></div></p>
<h3 id="_suggestion-list-and-documentation-side-by-side">Suggestion list and documentation side by side<a href="#_suggestion-list-and-documentation-side-by-side" target="_blank">#</a></h3>
<p>When IntelliSense autocomplete/suggestions are triggered, press ⌃Space to view the documentation for the suggestion item in focus as before. The documentation will now expand to the side instead of being overlaid on the suggest widget, enabling you to read the documentation and navigate the list at the same time.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/suggest.gif" alt="auto expanded docs in autocomplete" /></div></p>
<p>When the documentation fly-out is expanded, it will stay expanded (across VS Code windows, sessions and updates) every time autocomplete/suggestions is triggered, until you explicitly close it either using the close button or by pressing ⌃Space again.</p>
<p>For keyboard centric users who want to navigate up and down long documentation, press ⌃⌥Space to move the focus to the documentation fly-out such that it can now receive keyboard shortcuts for Page Up/Down actions.</p>
<p>For screen reader users, once the documentation fly-out is expanded, navigating the suggestion list will read out the label and documentation (if any) of the item in focus.</p>
<h3 id="_emmet-abbreviation-expansion-in-suggestion-list">Emmet abbreviation expansion in suggestion list<a href="#_emmet-abbreviation-expansion-in-suggestion-list" target="_blank">#</a></h3>
<p>Until now, the default behavior for expanding an Emmet expansion has been to use the Tab key. There were two issues with this design:</p>
<ul>
<li>Many unexpected Emmet expansions occurred when the user wanted to just add an indent.</li>
<li>On the other hand, items from the suggestion list got inserted when the user was expecting the Emmet abbreviation to be expanded.</li>
</ul>
<p>Both of these issues can be now solved by having the expanded Emmet abbreviations show up in the suggestion list and freeing up the Tab key for what it was meant to do, indenting.</p>
<p>Set <code>emmet.useNewEmmet</code> to <code>true</code> to start using this new feature. This feature is best used with the suggestion documentation fly-out expanded where you can preview the expanded abbreviation as you type. Note that Tab key will no longer expand the abbreviation by default.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/emmet.gif" alt="Emmet abbreviation expansion in autocomplete" /></div></p>
<p>If you have <code>editor.quickSuggestions</code> turned off, you can use one of the methods below to get Emmet expansion:</p>
<ul>
<li>Manually trigger the suggestion by pressing ⌃Space and then choose the expansion from the suggestion list.</li>
<li>Run the command <strong>Emmet: Expand Abbreviation</strong> explicity from the <strong>Command Palette</strong>.</li>
<li>Bind your own keyboard <a href="https://code.visualstudio.com/docs/getstarted/keybindings" target="_blank">shortcut</a> to <strong>Emmet: Expand Abbreviation</strong> (command id <code>editor.emmet.action.expandAbbreviation</code>).</li>
</ul>
<p>You will see two kinds of suggestions in HTML-like files:</p>
<ul>
<li>The expansion for the abbreviation that has been typed (you can turn this off by setting <code>emmet.showExpandedAbbreviation</code> to <code>false</code>).</li>
<li>All possible abbreviations whose prefix is the text that has been typed (you can turn this off by setting <code>emmet.showAbbreviationSuggestions</code> to <code>false</code>). For example, <code>a</code>, <code>a:link</code>, <code>a:mail</code>, <code>area</code> are suggested when you type <code>a</code>. This is helpful for discovering Emmet abbreviations.</li>
</ul>
<p>In CSS/LESS/SCSS files, you will only see the single abbreviation you have typed.</p>
<p>To implement this feature, we replaced the single monolithic <a href="https://github.com/emmetio/emmet" target="_blank">Emmet library</a> with smaller re-usable <a href="https://www.npmjs.com/%7Eemmetio" target="_blank">Emmet modules</a>. In doing so, most of the Emmet commands were re-implemented. If you see any changes in the behavior of any Emmet commands, please create an issue. We hope to complete this work in the next milestone, after which the setting <code>emmet.useNewEmmet</code> will be deprecated and the new model will be made default.</p>
<h3 id="_multi-cursor-snippets">Multi cursor snippets<a href="#_multi-cursor-snippets" target="_blank">#</a></h3>
<p>You can now combine snippets and multiple cursors.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/snippets-multi-cursor.gif" alt="multi cursor snippets" /></div></p>
<p>In addition, you also now nest snippets, meaning you can add a placeholder of a snippet within another snippet and their placeholders will be merged.</p>
<h3 id="_strict-snippets">Strict snippets<a href="#_strict-snippets" target="_blank">#</a></h3>
<p>Snippets can have placeholders and variables. The snippet syntax is defined <a href="https://code.visualstudio.com/docs/editor/userdefinedsnippets#_snippet-syntax" target="_blank">here</a> where <code>$1, $2...</code> are tabstops and <code>$varName1, $varName2...</code> are variables. Note that they can only differ by what follows the <code>$</code>-sign, numbers are tabstops and words refer to variables. Prior to this milestone, VS Code was using an internal syntax for snippets. Textmate-style snippets were rewritten to the internal syntax and there was an unfortunate bug that caused variables to be turned into tabstops. This is what we have done to ensure a smooth transition:</p>
<ul>
<li>When we encounter snippets that use variables we don't <a href="https://code.visualstudio.com/docs/editor/userdefinedsnippets#_variables" target="_blank">know</a>, we turn them into placeholders and warn the extension author (not the end user).</li>
<li>Also, we log a telemetry event so can make issues/PRs against extensions that are using this unfortunate construct.</li>
</ul>
<p>In the future, you can expect us to continue to support these types of snippets for a little longer. Snippets fall into two categories; those that the user created and those that come from an extension. We will be strict on extension snippets while keeping support for user created snippets.</p>
<h3 id="_find-widget">Find widget<a href="#_find-widget" target="_blank">#</a></h3>
<p>You can now resize the Find widget horizontally. You can review the full text easily if it's longer than the original width of the Find widget.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/resize-find-widget.gif" alt="Resize Find widget" /></div></p>
<p>Also you can now scroll beyond the first line when the Find widget is visible and the Find widget won't cover the matched results. We'll automatically scroll the window a little bit to make sure the matched results are not covered by the Find widget when you are navigating between them.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/uncover-matched-results.gif" alt="Uncover matched results" /></div></p>
<p>We introduced two settings to help you customize the Find widget behaviors:</p>
<ul>
<li>You can now set <code>editor.find.seedSearchStringFromSelection</code> to <code>false</code> if you don't want to seed the search string in Find widget from current editor selection.</li>
<li>You can set <code>editor.find.autoFindInSelection</code> to <code>true</code> and then Find in Selection flag is turned on when multiple characters or lines of text are selected in the editor.</li>
</ul>
<p>We also added a new command <code>toggleFindInSelection</code> (⌥⌘L) to toggle Find In Selection so you can keep your hands on the keyboard when switching all Find options.</p>
<h3 id="_folding-controls">Folding controls<a href="#_folding-controls" target="_blank">#</a></h3>
<p>The visibility of the folding controls next to the line numbers can now be configured by the setting <code>editor.showFoldingControls</code>:</p>
<ul>
<li><code>mouseover</code> - The existing behavior where controls for non-collapsed regions are hidden unless the mouse cursor is over the editor gutter.</li>
<li><code>always</code>- Folding controls are always shown.</li>
</ul>
<h3 id="_letter-spacing">Letter spacing<a href="#_letter-spacing" target="_blank">#</a></h3>
<p>Thanks to <a href="https://github.com/hoovercj" target="_blank">@hoovercj</a> in <a href="https://github.com/Microsoft/vscode/pull/22979" target="_blank">PR #22979</a>, there is a new editor setting, <code>editor.letterSpacing</code>, similar to the CSS letter-spacing property:</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/letter-spacing.gif" alt="letter spacing" /></div></p>
<h2 id="_integrated-terminal">Integrated Terminal<a href="#_integrated-terminal" target="_blank">#</a></h2>
<h3 id="_dragging-files-to-the-terminal-to-paste-path">Dragging files to the terminal to paste path<a href="#_dragging-files-to-the-terminal-to-paste-path" target="_blank">#</a></h3>
<p>You can now drag files and folder from the File Explorer and files from your OS file manager to paste the path name into the terminal.</p>
<h3 id="_unicode-character-width-improvements">Unicode character width improvements<a href="#_unicode-character-width-improvements" target="_blank">#</a></h3>
<p>Unicode characters in the Integrated Terminal are now sized explicitly which means that applications like <a href="https://www.npmjs.com/package/vtop" target="_blank">vtop</a> which make extensive use of these characters should now render correctly.</p>
<p>Before:</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/terminal-vtop-before.png" alt="Better unicode width before" /></div></p>
<p>After:</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/terminal-vtop-after.png" alt="Better unicode width after" /></div></p>
<h2 id="_tasks">Tasks<a href="#_tasks" target="_blank">#</a></h2>
<h3 id="_run-tasks-in-the-integrated-terminal">Run tasks in the Integrated Terminal<a href="#_run-tasks-in-the-integrated-terminal" target="_blank">#</a></h3>
<p>You can now configure tasks so that they are executed inside the Integrated Terminal. By adding a <code>runner</code> property to the <code>task.json</code> file as shown below you enable the Integrated Terminal.</p>
<pre><code>{
  "version": "0.1.0",
  "runner": "terminal",
  ...
}
</code></pre>
<p>If you want to switch back to the old runner, remove the property or set its value to <code>"process"</code>.</p>
<h3 id="_preview-tasks-version-20">Preview: Tasks version 2.0<a href="#_preview-tasks-version-20" target="_blank">#</a></h3>
<p>You can opt into the new tasks version 2.0.0 but please note that this version is currently a preview and still under active development. We make it available in order to get early feedback.</p>
<p>To enable the tasks preview, set the <code>version</code> attribute to <code>"2.0.0"</code> :</p>
<pre><code>{
  "version": "2.0.0"
}
</code></pre>
<p>With version 2.0.0 enabled, the tasks from different task runners like Gulp or Grunt are automatically detected and you can run them with the <code>Run Task</code> command. Tasks are currently auto detected from the task runners Gulp, Grunt, Jake, and from the scripts section in <code>package.json</code> files. We will provide an API so that you can contribute task detection for other task runners. This API has been further polished during this iteration, but we left in in the proposed state for this release (see <a href="https://github.com/Microsoft/vscode/blob/master/src/vs/vscode.proposed.d.ts#L13" target="_blank">vscode.proposed.d.ts</a>).</p>
<p>The task selection dialog now shows you both tasks that you have configured in the <code>task.json</code> file and tasks that where automatically detected. For example, in a workspace with a gulp file defining a <code>build</code> and a <code>watch</code> task and a <code>task.json</code> file that defines a <code>Deploy</code> task, the task selection dialog looks as follows:</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/task-selection.png" alt="task selection" /></div></p>
<p>When the system detects a task (for example, a build task provided through a gulp file), it usually doesn't know which problem matchers to associate with the task. You can customize a detected task inside the <code>tasks.json</code> file. To do so, press the gear icon to the right of a detected task. This will insert a section into the <code>tasks.json</code> file where you can customize the detected task.</p>
<p>The video below illustrates how to customize the gulp <code>build</code> task by adding the TypeScript problem matcher (named <code>$tsc</code>) to it and by renaming it to <code>My Main Build</code>.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/task-customize.gif" alt="task customize" /></div></p>
<h2 id="_debugging">Debugging<a href="#_debugging" target="_blank">#</a></h2>
<h3 id="_improved-stepping-performance">Improved stepping performance<a href="#_improved-stepping-performance" target="_blank">#</a></h3>
<p>Per a <a href="https://github.com/Microsoft/vscode/issues/25605" target="_blank">user recommendation</a>, we've improved stepping performance by fetching parts of the call stack and the corresponding variables lazily, only if the user has not already requested the next "step" operation. With this change, VS Code will always fetch the top frame of the stack in order to be able to show the correct source for the current location. The rest of the stack will be updated only if the user has not continued stepping for 0.4 seconds.</p>
<p>This improves stepping performance considerably as you can see in the following screen recordings of the (rather large) <a href="https://github.com/Microsoft/TypeScript" target="_blank">Typescript compiler</a>.</p>
<p>Old behavior - Always fetch full call stack:</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/step-before.gif" alt="step before" /></div></p>
<p>New behavior - Fetch rest of the call stack lazily:</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/step-after.gif" alt="step after" /></div></p>
<h3 id="_file-link-detection-in-exception-peek-ui">File link detection in Exception Peek UI<a href="#_file-link-detection-in-exception-peek-ui" target="_blank">#</a></h3>
<p>When an exception occurs, developers commonly follow through the exception stack trace to understand what caused it. We added a mechanism to detect links in the stack trace returned by the debug adapter. This allows you to jump to your source code straight from the exception UI. Moreover, it also improved existing link detection in a Debug Console, fixing several the user reported issues.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/exception-link-detection.png" alt="File Link Detection in Exception Peek UI" /></div></p>
<h3 id="_recipes-for-nonstandard-debugging-scenarios">Recipes for nonstandard debugging scenarios<a href="#_recipes-for-nonstandard-debugging-scenarios" target="_blank">#</a></h3>
<p>Setting up Node.js debugging can be challenging for some non-standard or complex scenarios. With this release, we've started to collect recipes for these scenarios in a new <a href="https://github.com/Microsoft/vscode-recipes" target="_blank">repository</a>.</p>
<p>The initial recipes cover <a href="https://github.com/Microsoft/vscode-recipes/tree/master/Docker-TypeScript" target="_blank">Debugging TypeScript in a Docker Container</a> and <a href="https://github.com/Microsoft/vscode-recipes/tree/master/MERN-Starter" target="_blank">Developing the MERN Starter in VS Code</a>.</p>
<h3 id="_copy-all-action-in-debug-console">Copy All action in Debug Console<a href="#_copy-all-action-in-debug-console" target="_blank">#</a></h3>
<p>It is now possible to copy all the content from the Debug Console using the <strong>Copy All</strong> context menu action. More details about what motivated this change can be found <a href="https://github.com/Microsoft/vscode/issues/2163" target="_blank">here</a>.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/copy-all.png" alt="copy all" /></div></p>
<h3 id="_new-setting-debuginternalconsoleoptions">New setting <code>debug.internalConsoleOptions</code><a href="#_new-setting-debuginternalconsoleoptions" target="_blank">#</a></h3>
<p>It is now possible to control the behavior of the Debug Console using the setting <code>debug.internalConsoleOptions</code>. Previously this setting was only available in <code>launch.json</code>, however by <a href="https://github.com/Microsoft/vscode/issues/18398" target="_blank">user request</a>, it is now possible to also specify this in user and workspace settings. The setting in <code>launch.json</code> takes precedence if both are provided.</p>
<h2 id="_node-debugging">Node Debugging<a href="#_node-debugging" target="_blank">#</a></h2>
<h3 id="_localremote-path-mapping-now-supported-for-launch-configurations">Local/remote path mapping now supported for "launch" configurations<a href="#_localremote-path-mapping-now-supported-for-launch-configurations" target="_blank">#</a></h3>
<p>To facilitate remote debugging, VS Code already supports mapping JavaScript paths between a local VS Code project and a (remote) location by means of the <code>localRoot</code> and <code>remoteRoot</code> attributes. Because remote debugging typically involves "attaching" to a remote target, the <code>localRoot</code> and <code>remoteRoot</code> attributes were only available for launch configurations of request type <code>"attach"</code>.</p>
<p>Recently we've opened up launch configurations of request type <code>"launch"</code> to launch arbitrary programs and scripts (and not just the local Node.js target to debug). With this, it becomes possible to launch a remote Node.js target (for example in a Docker container) and have the VS Code Node.js Debugger attach to it. This feature diminishes the difference between "launching" and "attaching" even further and it makes sense to support <code>localRoot</code> and <code>remoteRoot</code> attributes for launch configurations of request type <code>"launch"</code> as well (in addition to request type <code>"attach"</code>).</p>
<p>You can find an example for this in the <a href="https://github.com/Microsoft/vscode-recipes/tree/master/Docker-TypeScript#further-simplifying-the-debugging-setup" target="_blank">Debugging TypeScript in a Docker Container</a> recipe.</p>
<h2 id="_extensions">Extensions<a href="#_extensions" target="_blank">#</a></h2>
<h3 id="_enable-disable-commands">Enable / Disable commands<a href="#_enable-disable-commands" target="_blank">#</a></h3>
<p>There are two new commands in the <strong>Extensions</strong> view context menu to help quickly manage your extensions:</p>
<ul>
<li>Enable / Disable All Installed Extensions</li>
<li>Enable / Disable Auto Updating Extensions</li>
</ul>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/extensions-actions.png" alt="Extensions actions" /></div></p>
<h2 id="_languages">Languages<a href="#_languages" target="_blank">#</a></h2>
<h3 id="_syntax-coloring-for-jsxtsx-components">Syntax coloring for JSX/TSX components<a href="#_syntax-coloring-for-jsxtsx-components" target="_blank">#</a></h3>
<p>In React JSX and TSX files, component classes are now colored differently than normal HTML elements:</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/jsx-new-coloring.png" alt="new jsx coloring" /></div></p>
<h3 id="_additional-jsdoc-tags-in-hover-and-suggestions">Additional JSDoc tags in hover and suggestions<a href="#_additional-jsdoc-tags-in-hover-and-suggestions" target="_blank">#</a></h3>
<p>JSDoc tags such as <code>@deprecated</code> and <code>@private</code> are now displayed in hover and suggestions documentation.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/jsdocs.png" alt="JSDocs tags sections" /></div></p>
<h3 id="_open-ts-server-log-reveals-log-folder">Open TS Server Log reveals log folder<a href="#_open-ts-server-log-reveals-log-folder" target="_blank">#</a></h3>
<p>The <strong>TypeScript: Open TS Server Log</strong> command now reveals the TypeScript log directory on your operating system instead of trying to open the log file in VS Code. This is useful for collecting the additional Type Declaration (typings) installer log files generated alongside the main <code>tsserver.log</code> file.</p>
<h3 id="_markdown-preview-preserves-scroll-position">Markdown preview preserves scroll position<a href="#_markdown-preview-preserves-scroll-position" target="_blank">#</a></h3>
<p>The Markdown preview, along with other webview based views such as the release notes, will now preserve the scroll position when switching between editors. Previously, navigating away from the Markdown Preview and then returning to it caused the scroll position to be reset.</p>
<h3 id="_warnings-for-missing-markdown-preview-styles">Warnings for missing Markdown preview styles<a href="#_warnings-for-missing-markdown-preview-styles" target="_blank">#</a></h3>
<p>We now display a warning message if any of the stylesheets from <code>markdown.styles</code> used in the preview cannot be found.</p>
<h3 id="_markdown-symbol-search-includes-heading-levels">Markdown symbol search includes heading levels<a href="#_markdown-symbol-search-includes-heading-levels" target="_blank">#</a></h3>
<p>You can quickly jump to a heading in a Markdown file using <strong>Go to Symbol in File...</strong> (⇧⌘O). This list now includes the heading level of each symbol, which allows you to quickly filter results by heading level.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/markdown-heading-levels.png" alt="markdown symbols with header level" /></div></p>
<h2 id="_extension-authoring">Extension Authoring<a href="#_extension-authoring" target="_blank">#</a></h2>
<h3 id="_custom-views">Custom views<a href="#_custom-views" target="_blank">#</a></h3>
<p>There has been a popular request to customize VS Code to show custom data views, for example a <code>Node Dependencies</code> view. With this release, you can now write extensions to VS Code contributing such views. Currently custom views are shown only in Explorer. In future, we will support displaying them in other places too.</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/views.png" alt="Custom view" /></div></p>
<p>Contributing a view is as simple as follows:</p>
<ul>
<li>Contribute a view using the <a href="https://code.visualstudio.com/docs/extensionAPI/extension-points#_contributesviews" target="_blank">views</a> extension point.</li>
<li>Register a data provider for the view using the <a href="https://code.visualstudio.com/docs/extensionAPI/vscode-api#_TreeDataProvider" target="_blank">TreeDataProvider</a> API.</li>
<li>Contribute actions to the view using <code>view/title</code> and <code>view/item/context</code> locations in <a href="https://code.visualstudio.com/docs/extensionAPI/extension-points#_contributesmenus" target="_blank">menus</a> extension point.</li>
</ul>
<p>You can refer to examples in our <a href="https://github.com/Microsoft/vscode-extension-samples/tree/master/tree-view-sample" target="_blank">extension samples repository</a>.</p>
<h3 id="_debugger-extensions">Debugger extensions<a href="#_debugger-extensions" target="_blank">#</a></h3>
<p><strong>New enum value <code>subtle</code> for the <code>presentationHint</code> attribute of type <code>StackFrame</code></strong></p>
<p>A debug adapter can flag a stack frame with the presentation hint <code>subtle</code> in order to receive an alternative "subtle" rendering.</p>
<p><strong>Extended type for <code>TerminatedEvent.body.restart</code> attribute</strong></p>
<p>The type of the <code>TerminatedEvent.body.restart</code> attribute has been extended from <code>boolean</code> to <code>any</code>. This makes it possible to loop arbitrary data from one debug session to the next (restarted) debug session.</p>
<p><strong><code>evaluateName</code> attribute mandatory for <code>Add to Watch</code> and <code>Copy Value</code> actions</strong></p>
<p>VS Code previously tried to implement the <strong>Add to Watch</strong> and <strong>Copy Value</strong> actions by using the data from the <strong>VARIABLES</strong> view and a JavaScript-biased heuristic for building expressions that can be used with the evaluate request.</p>
<p>Since this approach does not work for all languages, we've introduced the <code>evaluateName</code> attribute for variables some time ago. It is now mandatory for debug adapters to support the <code>evaluateName</code> attribute if they want that <strong>Add to Watch</strong> and <strong>Copy Value</strong> actions work properly.</p>
<h3 id="_glob-patterns-for-workspacecontains-activation-event">Glob patterns for <code>workspaceContains</code> activation event<a href="#_glob-patterns-for-workspacecontains-activation-event" target="_blank">#</a></h3>
<p>Thanks to <a href="https://github.com/eamodio" target="_blank">@eamodio</a>, with <a href="https://github.com/Microsoft/vscode/pull/24570" target="_blank">PR #24570</a>, it is now possible to activate an extension when a folder is opened that contains at least one file that matches a glob pattern.</p>
<p>For example, an extension with the <code>package.json</code>:</p>
<pre><code>{
  ...
  "activationEvents": [
    "workspaceContains:**/.editorconfig"
  ]
}
</code></pre>
<p>will be activated when a folder is opened and any of its sub-folders contains a file named <code>.editorconfig</code>.</p>
<h3 id="_defining-a-languages-word-pattern-in-the-language-configuration-file">Defining a language's word pattern in the language configuration file<a href="#_defining-a-languages-word-pattern-in-the-language-configuration-file" target="_blank">#</a></h3>
<p>Thanks to <a href="https://github.com/hoovercj" target="_blank">@hoovercj</a>, with <a href="https://github.com/Microsoft/vscode/pull/22478" target="_blank">PR #22478</a>, it is possible to specify a language's word pattern using <code>wordPattern</code> in the language configuration file. This used to be possible before only by invoking <code>vscode.languages.setLanguageConfiguration(...)</code>.</p>
<h3 id="_better-control-decorations-in-the-editor">Better control decorations in the editor<a href="#_better-control-decorations-in-the-editor" target="_blank">#</a></h3>
<p>Thanks to <a href="https://github.com/CoenraadS" target="_blank">@CoenraadS</a>, with <a href="https://github.com/Microsoft/vscode/pull/25776" target="_blank">PR #25776</a>, it is now possible to configure the behavior of decorations when typing/editing at their edges. This can be configured with the <code>DecorationRenderOptions.rangeBehaviour</code> field.</p>
<h3 id="_reference-theme-colors-from-extensions">Reference theme colors from extensions<a href="#_reference-theme-colors-from-extensions" target="_blank">#</a></h3>
<p>You can now use theme colors in decorators and for the Status Bar foreground. Using theme colors instead of actual color values is the preferred way as it lets themes and users customize the colors.</p>
<pre><code>  var decorationType = vscode.window.createTextEditorDecorationType({
      before: {
          contentText: "\u26A0",
          color: new vscode.ThemeColor('editorWarning.foreground')
      }
  });
</code></pre>
<p>You will find the list of theme colors <a href="https://code.visualstudio.com/docs/getstarted/theme-color-reference" target="_blank">here</a>.</p>
<h2 id="_accessibility">Accessibility<a href="#_accessibility" target="_blank">#</a></h2>
<h3 id="_better-nvda-support">Better NVDA support<a href="#_better-nvda-support" target="_blank">#</a></h3>
<p>Sometimes, when using arrow keys, some lines or characters would be repeated by NVDA (see <a href="https://github.com/Microsoft/vscode/issues/26730" target="_blank">Issue #26730</a>). Thanks to <a href="https://github.com/jcsteh" target="_blank">James Teh</a>, one of the co-founders of <a href="https://www.nvaccess.org/" target="_blank">NV Access</a>, we now understand the root cause (a timeout of 30ms, which we sometimes miss). James has a <a href="https://github.com/nvaccess/nvda/pull/7201" target="_blank">PR on NVDA</a> where he is changing the default timeout to 100ms and making it configurable. Until a new NVDA version is shipped, thanks to <a href="https://github.com/derekriemer" target="_blank">Derek Riemer</a>, there is an <a href="https://files.derekriemer.com/globalEditorTimer-1.0.nvda-addon" target="_blank">NVDA plugin</a> that increases the timeout from 30ms to 200ms. We have also done some changes on our side to reduce the likelihood that we miss the 30ms timeout.</p>
<h3 id="_screen-reader-detected">"Screen Reader Detected"<a href="#_screen-reader-detected" target="_blank">#</a></h3>
<p>We are now leveraging <a href="https://github.com/electron/electron/blob/master/docs/api/app#_event-accessibility-support-changed-macos-windows" target="_blank">Electron APIs</a> to react and optimize VS Code when working with a screen reader. Whenever Electron identifies that a screen reader is attached, we will display a message in the Status Bar and:</p>
<ul>
<li>Remove the Line Number and Column indicator from the Status Bar, as we have found updating these indicators causes a myriad of accessibility events that end up confusing screen readers.</li>
<li>Disable word wrapping, as when pressing arrow down for example, screen readers expect the cursor to move to the next line and not to a column to the right on the same line.</li>
<li>Mirror the current page of text in the editor synchronously to the <code>&lt;textarea&gt;</code> we use for input events.</li>
<li>Disable certain stylistic features to increase the likelihood that we make it within the 30ms accessibility event timeout. We typically do not spend more than ~4-5ms processing the arrow keys, but with these features disabled, the time spent is reduced to ~1-2ms. The rest of the time is spent by our platform in <em>figuring out</em> what happened and emitting the correct accessibility events.</li>
</ul>
<blockquote>
<p>Detecting screen readers is non-trivial, so, if you notice the "Screen Reader Detected" Status Bar message and do not have a screen reader attached, you can change the setting <code>editor.accessibilitySupport</code> from <code>"auto"</code> to <code>"off"</code>.</p>
</blockquote>
<h2 id="_engineering">Engineering<a href="#_engineering" target="_blank">#</a></h2>
<h3 id="_new-crash-report-handling">New crash report handling<a href="#_new-crash-report-handling" target="_blank">#</a></h3>
<p>We have improved the VS Code crash reporting. VS Code uses Electron's built-in crash reporter to capture and analyze crash data to make VS Code and Electron itself better. If VS Code crashes, a dump is collected and sent to us, though <a href="https://code.visualstudio.com/docs/supporting/faq#_how-to-disable-crash-reporting" target="_blank">you can always turn this off</a>.</p>
<p>This worked well, but it was a time consuming task for us to analyze and understand a crash. Microsoft has a good crash reporting service called <a href="https://hockeyapp.net/" target="_blank">HockeyApp</a> and we now have enabled HockeyApp for crash reporting. To enable it, we had to produce our own build of Electron because the built-in crash reporter sends data in a format HockeyApp does not understand. The changes are on top of Electron 1.6.6 where the crash reporter talks to the HockeyApp service.</p>
<p>If you build VS Code from source, you will continue to pull in the GitHub version of Electron. We will continue collaborating with the other Electron contributors to make the crash reporting service pluggable, so that anyone can easily use HockeyApp (or any other service).</p>
<h3 id="_issue-management-automation">Issue management automation<a href="#_issue-management-automation" target="_blank">#</a></h3>
<p>We have deployed a <a href="https://github.com/probot/probot" target="_blank">Probot</a> instance to automate some of our issue management. You will see <code>VSCodeBot</code> add labels to issues on GitHub and sometimes close issues when they have gone stale. We are looking for feedback from the community and will add more automation as we go.</p>
<p>Adding an <code>insiders</code> label to an issue reported against an <a href="https://code.visualstudio.com/insiders" target="_blank">Insiders</a> build:</p>
<p><img src="/assets/updates/1_13/bot-labels-insiders.png" alt="VSCodeBot labels issues reported against Insiders build" /></p>
<p>Closing a stale <code>needs more info</code> issue after we haven't heard back for more than week:</p>
<p><div class="readableLargeImageContainer"><img src="/assets/updates/1_13/bot-closes-needs-more-info.png" alt="VSCodeBot closes stale  issue" /></div></p>
<h3 id="_automated-smoke-test">Automated Smoke Test<a href="#_automated-smoke-test" target="_blank">#</a></h3>
<p>As part of this milestone, we automated the <a href="https://github.com/Microsoft/vscode/wiki/Smoke-Test" target="_blank">Smoke Test</a> that we used to perform manually each release. All manual steps were automated with the use of the <a href="https://electron.atom.io/spectron" target="_blank">Spectron</a> testing framework with detailed progress tracked in <a href="https://github.com/Microsoft/vscode/issues/25291" target="_blank">this issue</a>.</p>
<p>The Smoke Test assists us in verifying whether all VS Code basic features are working before publishing a release. Automating the test enables us to save time on testing and put more resources and focus on the development of new features.</p>
<h2 id="_new-commands">New Commands<a href="#_new-commands" target="_blank">#</a></h2>
<table>
<thead>
<tr>
<th>Key</th>
<th>Command</th>
<th>Command id</th>
</tr>
</thead>
<tbody>
<tr>
<td>unassigned</td>
<td>Select first child of currently selected item's parent in tree/lists</td>
<td><code>list.focusFirstChild</code></td>
</tr>
<tr>
<td>unassigned</td>
<td>Select last child of currently selected item's parent in tree/lists</td>
<td><code>list.focusLastChild</code></td>
</tr>
<tr>
<td>unassigned</td>
<td>Next Merge Conflict</td>
<td><code>merge-conflict.next</code></td>
</tr>
<tr>
<td>unassigned</td>
<td>Previous Merge Conflict</td>
<td><code>merge-conflict.previous</code></td>
</tr>
<tr>
<td>unassigned</td>
<td>Accept Selection</td>
<td><code>merge-conflict.accept.selection</code></td>
</tr>
<tr>
<td>unassigned</td>
<td>Accept Current</td>
<td><code>merge-conflict.accept.current</code></td>
</tr>
<tr>
<td>unassigned</td>
<td>Accept Incoming</td>
<td><code>merge-conflict.accept.incoming</code></td>
</tr>
<tr>
<td>unassigned</td>
<td>Accept Both</td>
<td><code>merge-conflict.accept.both</code></td>
</tr>
<tr>
<td>unassigned</td>
<td>Accept All Both</td>
<td><code>merge-conflict.accept.all-both</code></td>
</tr>
<tr>
<td>unassigned</td>
<td>Accept All Current</td>
<td><code>merge-conflict.accept.all-current</code></td>
</tr>
<tr>
<td>unassigned</td>
<td>Accept All Incoming</td>
<td><code>merge-conflict.accept.all-incoming</code></td>
</tr>
<tr>
<td>unassigned</td>
<td>Compare</td>
<td><code>merge-conflict.compare</code></td>
</tr>
</tbody>
</table>
<h2 id="_contributions-to-extensions">Contributions to Extensions<a href="#_contributions-to-extensions" target="_blank">#</a></h2>
<p>Our team maintains or contributes to a number of VS Code extensions. Most notably this month:</p>
<ul>
<li><a href="https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint" target="_blank">ESLint</a>: Performance improvements to lower CPU load when linting large JavaScript files with lots of code actions.</li>
<li><a href="https://marketplace.visualstudio.com/items?itemName=vscodevim.vim" target="_blank">VSCodeVim</a>: We <a href="https://github.com/VSCodeVim/Vim/pull/1642" target="_blank">refactored</a> the source code to make it easier to contribute to the project.</li>
<li><a href="https://github.com/felixfbecker/php-language-server" target="_blank">PHP language server</a>: We are getting close to merging the <a href="https://github.com/felixfbecker/php-language-server/pull/357" target="_blank">pull request</a> to adopt the <a href="https://github.com/Microsoft/tolerant-php-parser" target="_blank">tolerant PHP parser</a>.</li>
</ul>
<h2 id="_notable-changes">Notable Changes<a href="#_notable-changes" target="_blank">#</a></h2>
<ul>
<li><a href="https://github.com/Microsoft/vscode/issues/25789" target="_blank">25789</a>: Can't split file when dragging from Explorer</li>
<li><a href="https://github.com/Microsoft/vscode/issues/19644" target="_blank">19644</a>: Cursor does not go to the maximum line column when pressing "End" twice with word wrap enabled</li>
<li><a href="https://github.com/Microsoft/vscode/issues/6661" target="_blank">6661</a>: Ctrl+D/Cmd+D merges adjacent selections.</li>
<li><a href="https://github.com/Microsoft/vscode/issues/4271" target="_blank">4271</a>: Mac Insert Emoji Duplicates Text</li>
<li><a href="https://github.com/Microsoft/vscode/issues/3623" target="_blank">3623</a>: Match whole word does not work for not latin characters (at least for cyrillic)</li>
<li><a href="https://github.com/Microsoft/vscode/issues/17534" target="_blank">17534</a>: Search: not possible to remove individual search results in a file</li>
<li><a href="https://github.com/Microsoft/vscode/issues/16580" target="_blank">16580</a>: Unable to write to settings should offer an action to open settings</li>
<li><a href="https://github.com/Microsoft/vscode/issues/17609" target="_blank">17609</a>: Line wrapping problem in bash on ubuntu on windows</li>
<li><a href="https://github.com/Microsoft/vscode/issues/23484" target="_blank">23484</a>: "Ctrl +click to follow link" hover appears only on the last link in the terminal</li>
<li><a href="https://github.com/Microsoft/vscode/issues/25664" target="_blank">25664</a>: Terminal panel is not properly restored after restarting</li>
</ul>
<h2 id="_thank-you">Thank You<a href="#_thank-you" target="_blank">#</a></h2>
<p>Last but certainly not least, a big <em><strong>Thank You!</strong></em> to the following folks that helped to make VS Code even better:</p>
<p>Contributions to <code>vscode</code>:</p>
<ul>
<li><a href="https://github.com/actboy168" target="_blank">actboy168 (@actboy168)</a>: Fix lua function colorizing error <a href="https://github.com/Microsoft/vscode/pull/26880" target="_blank">PR #26880</a></li>
<li><a href="https://github.com/andy-ms" target="_blank">Andy (@andy-ms)</a>:  Remove unnecessary parentheses <a href="https://github.com/Microsoft/vscode/pull/25573" target="_blank">PR #25573</a></li>
<li><a href="https://github.com/ashirley" target="_blank">@ashirley</a>: Add git.commitType configuration <a href="https://github.com/Microsoft/vscode/pull/25855" target="_blank">PR #25855</a></li>
<li><a href="https://github.com/bmeck" target="_blank">Bradley Meck (@bmeck)</a>:  Add .mjs to known JavaScript file extensions <a href="https://github.com/Microsoft/vscode/pull/25747" target="_blank">PR #25747</a></li>
<li><a href="https://github.com/BugraC" target="_blank">Bugra Cuhadaroglu (@BugraC)</a>:  Fix - #24242 #24550 <a href="https://github.com/Microsoft/vscode/pull/25756" target="_blank">PR #25756</a></li>
<li><a href="https://github.com/CoenraadS" target="_blank">@CoenraadS</a>:  Expose Stickiness API #15758 <a href="https://github.com/Microsoft/vscode/pull/25776" target="_blank">PR #25776</a></li>
<li><a href="https://github.com/dlech" target="_blank">David Lechner (@dlech)</a>:  Add .git/subtree-cache/ to files.watcherExclude <a href="https://github.com/Microsoft/vscode/pull/26665" target="_blank">PR #26665</a></li>
<li><a href="https://github.com/eamodio" target="_blank">Eric Amodio (@eamodio)</a>:  Fixes #944 - Support wildcards on activationEvents.workspaceContains <a href="https://github.com/Microsoft/vscode/pull/24570" target="_blank">PR #24570</a></li>
<li><a href="https://github.com/hoovercj" target="_blank">Cody Hoover (@hoovercj)</a>
<ul>
<li>Add letterSpacing to config to address #18715 <a href="https://github.com/Microsoft/vscode/pull/22979" target="_blank">PR #22979</a></li>
<li>Addresses #14221 by reading wordPattern from language-configuration.json <a href="https://github.com/Microsoft/vscode/pull/22478" target="_blank">PR #22478</a></li>
</ul>
</li>
<li><a href="https://github.com/hungys" target="_blank">Yu-Hsin Hung (@hungys)</a>:  Fix for terminal.foreground not working <a href="https://github.com/Microsoft/vscode/pull/26788" target="_blank">PR #26788</a></li>
<li><a href="https://github.com/ihalip" target="_blank">Ilie Halip (@ihalip)</a>
<ul>
<li>added config option git.cloneDirectory, defaulting to os.homedir() <a href="https://github.com/Microsoft/vscode/pull/24950" target="_blank">PR #24950</a></li>
<li>Allow changing a SourceControlResourceGroup's label <a href="https://github.com/Microsoft/vscode/pull/25983" target="_blank">PR #25983</a></li>
</ul>
</li>
<li><a href="https://github.com/Ikuyadeu" target="_blank">Yuki Ueda (@Ikuyadeu)</a>:  [bat] support %%(fix #26825) <a href="https://github.com/Microsoft/vscode/pull/27325" target="_blank">PR #27325</a></li>
<li><a href="https://github.com/JeremyLoy" target="_blank">Jeremy Loy (@JeremyLoy)</a>:  Added Services Submenu for MacOS <a href="https://github.com/Microsoft/vscode/pull/26248" target="_blank">PR #26248</a></li>
<li><a href="https://github.com/jhasse" target="_blank">Jan Niklas Hasse (@jhasse)</a>
<ul>
<li>Use Chromium's new system-ui font alias <a href="https://github.com/Microsoft/vscode/pull/25570" target="_blank">PR #25570</a></li>
<li>Use Tahoma font as a fallback for system-ui <a href="https://github.com/Microsoft/vscode/pull/26912" target="_blank">PR #26912</a></li>
</ul>
</li>
<li><a href="https://github.com/jportela" target="_blank">João Portela (@jportela)</a>
<ul>
<li>Preventing duplicate tab close when doing a middle click <a href="https://github.com/Microsoft/vscode/pull/25697" target="_blank">PR #25697</a></li>
<li>Inserting file path on the terminal, when dragging a file to it <a href="https://github.com/Microsoft/vscode/pull/24951" target="_blank">PR #24951</a></li>
</ul>
</li>
<li><a href="https://github.com/kdmu" target="_blank">Kaide Mu (@kdmu)</a>:  Markdown: Capture right parenthesis as part of url <a href="https://github.com/Microsoft/vscode/pull/26449" target="_blank">PR #26449</a></li>
<li><a href="https://github.com/letmaik" target="_blank">Maik Riechert (@letmaik)</a>
<ul>
<li>Show ahead/behind indicator while git syncing <a href="https://github.com/Microsoft/vscode/pull/26008" target="_blank">PR #26008</a></li>
<li>Add git delete branch command <a href="https://github.com/Microsoft/vscode/pull/25862" target="_blank">PR #25862</a></li>
</ul>
</li>
<li><a href="https://github.com/luxifer" target="_blank">Florent Viel (@luxifer)</a>
<ul>
<li>Fix php function highlight <a href="https://github.com/Microsoft/vscode/pull/26543" target="_blank">PR #26543</a></li>
<li>Add more tests to PHP grammar <a href="https://github.com/Microsoft/vscode/pull/26992" target="_blank">PR #26992</a></li>
</ul>
</li>
<li><a href="https://github.com/mappu" target="_blank">@mappu</a>:  extension/php: detect language via shebang <a href="https://github.com/Microsoft/vscode/pull/26581" target="_blank">PR #26581</a></li>
<li><a href="https://github.com/misoguy" target="_blank">Soo Jae Hwang (@misoguy)</a>:  Change behavior of home/end button <a href="https://github.com/Microsoft/vscode/pull/21338" target="_blank">PR #21338</a></li>
<li><a href="https://github.com/nicksnyder" target="_blank">Nick Snyder (@nicksnyder)</a>
<ul>
<li>Do not unregister themingParticipantChangeListener. <a href="https://github.com/Microsoft/vscode/pull/27098" target="_blank">PR #27098</a></li>
<li>Fix typo <a href="https://github.com/Microsoft/vscode/pull/25584" target="_blank">PR #25584</a></li>
<li>Make SearchWidget dependencies injectable <a href="https://github.com/Microsoft/vscode/pull/26969" target="_blank">PR #26969</a></li>
</ul>
</li>
<li><a href="https://github.com/pprice" target="_blank">Phil Price (@pprice)</a>:  Add better merge extension <a href="https://github.com/Microsoft/vscode/pull/27150" target="_blank">PR #27150</a></li>
<li><a href="https://github.com/rishii7" target="_blank">Rishii7 (@rishii7)</a>:  Add a new user configuration <code>extensions.ignoreRecommendations</code> <a href="https://github.com/Microsoft/vscode/pull/25038" target="_blank">PR #25038</a></li>
<li><a href="https://github.com/rokoroku" target="_blank">Youngrok Kim (@rokoroku)</a>:  Add feature to close TMScope inspector <a href="https://github.com/Microsoft/vscode/pull/26980" target="_blank">PR #26980</a></li>
<li><a href="https://github.com/seesemichaelj" target="_blank">Mike Seese (@seesemichaelj)</a>:  Issue 15613 all files committed <a href="https://github.com/Microsoft/vscode/pull/25364" target="_blank">PR #25364</a></li>
<li><a href="https://github.com/smoogipooo" target="_blank">Dan Balasescu (@smoogipooo)</a>: Expose status bar debugging and no-folder foreground colors. <a href="https://github.com/Microsoft/vscode/pull/27052" target="_blank">PR #27052</a></li>
<li><a href="https://github.com/the-ress" target="_blank">Tereza Tomcova (@the-ress)</a>:  Fixes #4370: Set default icon for file associations <a href="https://github.com/Microsoft/vscode/pull/25497" target="_blank">PR #25497</a></li>
<li><a href="https://github.com/thr0w" target="_blank">Fernando Tolentino (@thr0w)</a>:  IntelliSense in extensions file <a href="https://github.com/Microsoft/vscode/pull/26564" target="_blank">PR #26564</a></li>
<li><a href="https://github.com/tomoki1207" target="_blank">MaruyamaTomoki (@tomoki1207)</a>:  Markdown preview support the UNC path files. <a href="https://github.com/Microsoft/vscode/pull/26710" target="_blank">PR #26710</a></li>
<li><a href="https://github.com/tonsky" target="_blank">Nikita Prokopov (@tonsky)</a>
<ul>
<li>Detect more def* forms in Clojure syntax <a href="https://github.com/Microsoft/vscode/pull/25546" target="_blank">PR #25546</a></li>
<li>Capture regexp begin/end as punctuation in Clojure syntax <a href="https://github.com/Microsoft/vscode/pull/25550" target="_blank">PR #25550</a></li>
</ul>
</li>
<li><a href="https://github.com/wgrriffel" target="_blank">Wagner Riffel (@wgrriffel)</a>:  Lua syntax extension is missing 'goto' keyword <a href="https://github.com/Microsoft/vscode/pull/26350" target="_blank">PR #26350</a></li>
</ul>
<p>Contributions to <code>language-server-protocol</code>:</p>
<ul>
<li><a href="https://github.com/ktec" target="_blank">Keith (@ktec)</a>: Update protocol-1-x.md <a href="https://github.com/Microsoft/language-server-protocol/pull/244" target="_blank">PR #244</a></li>
<li><a href="https://github.com/RainerKlute" target="_blank">Rainer Klute (@RainerKlute)</a>
<ul>
<li>Various minor editorial changes <a href="https://github.com/Microsoft/language-server-protocol/pull/242" target="_blank">PR #242</a></li>
<li>Typo fixed <a href="https://github.com/Microsoft/language-server-protocol/pull/239" target="_blank">PR #239</a></li>
</ul>
</li>
<li><a href="https://github.com/CXuesong" target="_blank">Chen (@CXuesong)</a>: Fix typo in summary of <code>interface Registration</code>. <a href="https://github.com/Microsoft/language-server-protocol/pull/231" target="_blank">PR #231</a></li>
<li><a href="https://github.com/spoenemann" target="_blank">Miro Spönemann (@spoenemann)</a>: Fixed typo in WorkspaceClientCapabilities <a href="https://github.com/Microsoft/language-server-protocol/pull/225" target="_blank">PR #225</a></li>
</ul>
<p>Contributions to <code>vscode-languageserver-node</code>:</p>
<ul>
<li><a href="https://github.com/XVincentX" target="_blank">Vincenzo Chianese (@XVincentX)</a>: Detect and copy npm-shirkwrap file if present <a href="https://github.com/Microsoft/vscode-languageserver-node/pull/193" target="_blank">PR #193</a></li>
</ul>
<p>Contributions to <code>vscode-tslint</code>:</p>

<p>Contributions to <code>vscode-css-languageservice</code>:</p>

<p>Contributions to <code>vscode-chrome-debug-core</code>:</p>
<ul>
<li><a href="https://github.com/llgcode" target="_blank">@llgcode</a>: Enhance path matching. <a href="https://github.com/Microsoft/vscode-chrome-debug-core/pull/202" target="_blank">PR #202</a></li>
</ul>
<p>Contributions to <code>localization</code>:</p>
<p>This is second month since we opened community localization in Transifex. We now have more 200 members in the Transifex <a href="https://aka.ms/vscodeloc" target="_blank">VS Code project</a> team. We appreciate your contributions, either by providing new translations, voting on translations, or suggesting process improvements.</p>
<p>Here is a snapshot of top contributors for this release. For details about the project including the contributor name list, visit the project site at <a href="https://aka.ms/vscodeloc" target="_blank">https://aka.ms/vscodeloc.</a></p>
<ul>
<li><strong>French:</strong> Vincent Biret, JP Gouigoux, Julien Brochet.</li>
<li><strong>Italian:</strong> Aldo Donetti, Piero Azi, Luca Nardi, Giuseppe Pignataro.</li>
<li><strong>German:</strong> Levin Rickert, Ingo Bleile, Carsten Kneip, Christian Gräfe, Markus Weber.</li>
<li><strong>Spanish:</strong> Andy Gonzalez, Alberto Poblacion, José M. Aguilar, Juan Carlos Gonzalez Martin.</li>
<li><strong>Russian:</strong> Al Fes, Aleksey Nemiro, Orrchy, Serge Rodionov.</li>
<li><strong>Japanese:</strong> EbXpJ6bp, Yuichi Nukiyama, Yosuke Sano, Yuki Ueda, Takayoshi Tanaka, Tetsuya Fukuda, Takashi Kawasaki.</li>
<li><strong>Korean:</strong> Ian Y. Choi.</li>
<li><strong>Chinese (Simplified):</strong> Joel Yang, YF, Alan Tsai, 王韦煊, Jianfeng Fang, kui li.</li>
<li><strong>Chinese (Traditional):</strong> Alan Liu, Alan Tsai, Duran Hsieh, Wei-Ting(DM), JJJ.</li>
</ul>
<p>We would also like to congratulate and thank the Brazilian Portuguese community localization team! Due to their efforts, localization is now completed in Transifex and the translations have been integrated into the <a href="https://code.visualstudio.com/insiders" target="_blank">Insiders</a> build for testing. Depending on validation progress, we hope to soon integrate the translations into the stable builds for Brazilian customers.</p>
<ul>
<li><strong>Portuguese (Brazil):</strong> Roberto Fonseca, Bruno Sonnino, Alessandro Fragnani, Douglas Eccker, Bruno Ochotorena, Rodrigo Crespi, Anderson Santos, Felipe Caputo, Marcelo Fernandes, Roberto Nunes, Rodrigo Romano, Luan Moreno Medeiros Maciel, Ilton Sequeira.</li>
</ul>


			<div><div><div><h3>Was this documentation helpful?</h3></div>
		