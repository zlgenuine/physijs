Stopping simulation simply requires stopping the calling the simulate function when rendering (as shown below).

`
var render = function() {
    if (!isPaused) {
        scene.simulate();
    }
    renderer.render();
};
`

Resuming the simulation requires calling the onSimulationResume method of the scene which will set the last simulation time to be equal to the current time, preventing all the simulations which would've occurred if the simulation was not paused. This is shown below.
`
var unpauseSimulation = function() {
    isPaused = false;
    scene.onSimulationResume();
};
`