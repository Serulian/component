# Simple Component Framework

## Example Usage

```seru
from "github.com/Serulian/component" import RenderComponent, UpdateComponentState
from "github.com/Serulian/virtualdom" import Context, Div, Button, If, Span

function<void> StartApp(element Element) {
	RenderComponent(<App />, element)
}

/**
 * appState holds the state of the app.
 */
struct appState {
	displayingMessage bool
}

/**
 * App is the root component for the application.
 */
class App {
	var<appState> state

	constructor Declare() {
		return App{
			state: appState{
				displayingMessage: false,
			},
		}
	}

	function<void> StateUpdated(state any) {
		this.state = state.(appState)
	}

	function<void> showMessage() {
		UpdateComponentState(this, this.state{
			displayingMessage: true,
		})
	}

	function<any> Render(context Context) {
		return <Div id="rootElement">
					<Button onclick={this.showMessage} @If={!this.state.showingMessage}>
						Run
					</Button>
					<Span @If={this.state.showingMessage}>Hello World!</Span>
			   </Div>
	}
}

```