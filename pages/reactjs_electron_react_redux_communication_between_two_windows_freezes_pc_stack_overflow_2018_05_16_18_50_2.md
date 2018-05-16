<a href="https://stackoverflow.com/questions/40473768/electron-react-redux-communication-between-two-windows-freezes-pc">https://stackoverflow.com/questions/40473768/electron-react-redux-communication-between-two-windows-freezes-pc</a><div id="articleHeader"><h1>electron + react + redux communication between two windows freezes PC?</h1></div>

<p>I'm trying to update state in another window depedning on state changes in the first window but ipc communcation doesn't work as expected for me.</p>

<p>In my first window, I have:</p>

<pre><code>onStatsSelect(event, menuItem, index) {
    const selectedStatsCopy = this.state.selectedStats.slice();
    const itemIndex = selectedStatsCopy.indexOf(menuItem.props.primaryText);
    if (itemIndex &gt; -1) {
      delete selectedStatsCopy[itemIndex];
    } else {
      selectedStatsCopy[index] = menuItem.props.primaryText;
    }

    // Update state
    this.setState({ selectedStats: selectedStatsCopy });

    // Notify worker window of change
    if (!(this.props.isReport)) {
      console.log('in renderer main window');
      ipcRenderer.send("updateSelectedStatsMain", event, selectedStatsCopy);
    }
  }
</code></pre>

<p>This is a callback for updating selectedStats state. It will also notify worker window of this update as seen in the last lines. <code>if (!(this.props.isReport))</code> This is an important check since both windows share the same component and so I use property <code>isReport</code> to distinguish between the two.</p>

<p>In my main process, I have: </p>

<pre><code>  // Selected Stats have changed in main window
  ipcMain.on('updateSelectedStatsMain', (event, selectedStatsCopy) =&gt; {
    console.log('in main');
    // Send to worker window
    workerWindow.webContents.send('updateSelectedStatsRen', event, selectedStatsCopy);
  });
</code></pre>

<p>This code will communicate back to worker window with the new state <code>selectedStatsCopy</code>. </p>

<p>In my <code>comoponentDidMount</code>, I have:</p>

<pre><code>componentDidMount() {
    // Register listening to message in case this is the worker window
    if (this.props.isReport) {
      console.log('in renderer worker window');
      ipcRenderer.on("updateSelectedStatsRen", (event, selectedStatsCopy) =&gt; {
        console.log('in renderer worker window event');
        this.setState({ selectedStats: selectedStatsCopy });
      });
    }
  }
</code></pre>

<p>This is supposed to work but electron hangs at line <code>ipcRenderer.send("updateSelectedStatsMain", event, selectedStatsCopy);</code> making main window hangs for a while and it continues using resources until PC freezes. </p>

<p>What is the problem here? </p>
    