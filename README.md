This project provides three different methods for computing the equivalent transfer function G(s) = Y / U from a Simulink model.

1. computeEquivalentTF_symbolicBased.p - Extracts and solves symbolic equations to compute the transfer function directly
2. computeEquivalentTF_graphBased.p - Builds a signal flow graph from the Simulink model and applies Mason's Gain Formula
3. computeEquivalentTF_auto.p - Automatically attempts the symbolic-based method first; if the result is invalid or fails, it falls back to the graph-based approach
4. main.p - Interactive script that lets the user select the model and method from the console

Folder Structure

- computeEquivalentTF_symbolicBased.p
- computeEquivalentTF_graphBased.p
- computeEquivalentTF_auto.p
- main.p
- Model Examples — contains example Simulink models used by main.p

Requirements

- MATLAB (R2019b or newer recommended)
- Simulink
- Symbolic Math Toolbox

Usage

Make sure the folder containing these scripts is added to the MATLAB path (Right click on the folder -> Add To Path -> Selected Folders and Subfolders)

Option 1: Run the interactive script

    run main

This will display all .slx models located in the 'Model Examples' folder and ask you to select one along with the desired method. The script only searches for models inside that folder.

Option 2: Call one of the functions directly from the MATLAB command window

    Geq = computeEquivalentTF_auto('modelName');

In this case, modelName should be the name of the Simulink model (without the .slx extension). You can place the .slx file anywhere on the MATLAB path or in the current folder. The 'Model Examples' folder is not required when calling functions directly.

Example

For the provided example model Toy_example.slx:

    Geq = computeEquivalentTF_auto('Toy_example');

The result is a symbolic expression representing the equivalent transfer function. Messages in the command window will indicate which method was used and whether the symbolic computation was successful or not.

Notes

- The Simulink model must be SISO (Single Input Single Output)
- The model should have only one top-level Inport and one top-level Outport
- SubSystem blocks are not supported. If detected, a warning is issued and the result is set to NaN
- You may add your own models to the 'Model Examples' folder if you use the main.p interface
- If the symbolic approach fails or misses block parameters, the tool automatically switches to the graph-based method
- To test each method individually:

      [Geq_symbolic, blockSym] = computeEquivalentTF_symbolicBased('modelName');
      Geq_graph = computeEquivalentTF_graphBased('modelName');
