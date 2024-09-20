## User

This is the beginning of an individual meeting with Medicinal Chemist to discuss your research project.

Here is context for this meeting:

[begin context 1]

ExperimentBioLayerInterferometry[Samples]⟹Protocol

generates a Protocol object for performing Bio-Layer Interferometry (BLI) on the provided Samples.



Biolayer interferometry is a technique used to quantify the magnitude and kinetics of an interaction between a surface immobilized species and a solution phase analyte. Binding of the analyte is monitored by the change in thickness of the bound bio-layer on the tip of a fiber-optic probe, which is determined by the white-light interference pattern of a reference channel and the bio-layer/solution interface. Probe tips can be functionalized via immersion in a solution of the target immobilized species and regenerated to return either a loading ready or measurement ready surface. After appropriate treatment, the probes are dipped into a sample solution to quantify the analyte concentration or to determine the association and dissociation kinetics. Other common experiments include epitope binning and assay optimization. Biolayer interferometry is useful for studying a variety of interactions involving proteins, oligomers, small molecules, fragments, and antibodies, and can be performed on crude samples such as cell lysate.



Experimental Principles

Figure 1.1: Procedural overview of a Biolayer Interferometry experiment. Step 1: The assay plate is loaded with buffers, loading solutions, standards, analytes, and other types of solutions required for the desired assay. Step 2: The probes are loaded into the probe rack position, where they may be immersed in equilibration solution prior to and during the course of the assay. Step 3: The multi-channel reader probes are immersed in an assay plate column to load the probe surface with an immobilized species (ActivateSurface, LoadSurface, Quench), measure the analyte binding properties (MeasureAssociation, MeasureDissocaition, Quantitate), or return the probe to measurement-ready condition via regeneration (Regenerate, Neutralize, Wash). Step 4: Any solutions derived from a given sample can be recovered from the AssayPlate.



Instrumentation

Octet Red96e

Model[Instrument, BioLayerInterferometer, "id:xRO9n3Bw9ZRq"]

Figure 2.1.1: Fiber-optic probes are stored in the probe rack position, either dry or immersed in a buffer solution. An 8-channel manifold moves between the probe rack and assay plate positions to pick up probes and conduct measurements via immersion in wells of a given column in the assay plate. A plate cover can be used to cover columns of the assay plate not currently being measured by the 8-channel reader to prevent evaporation over the course of long assays. The white light input reflects off of the internal optical layer and the biolayer/solution interface, producing an interference pattern which is directly proportional to the biolayer thickness.



Experiment Options

General

Instrument

The device on which the bio-layer interferometry protocol is to be run.

Default Value: Model[Instrument, BioLayerInterferometer, Octet Red96e]

Pattern Description: An object of type or subtype Model[Instrument, BioLayerInterferometer] or Object[Instrument, BioLayerInterferometer]

Programmatic Pattern: ObjectP[{Model[Instrument, BioLayerInterferometer], Object[Instrument, BioLayerInterferometer]}]

ExperimentType

The objective of bio-layer interferometry experiment. Kinetics: Measure association and dissociation rates of the interaction between a solution phase species and a functionalized bio-probe surface. Quantitation: Quantify the amount of analyte in a solution by measuring the change in bio-layer thickness upon immersion of a functionalized bio-probe in a solution containing the target analyte. EpitopeBinning: Use competition experiments between two antibodies to identify groups of antibodies which bind a given antigen at the same epitope. AssayDevelopment: Optimize the bio-probe functionalization and individual assay steps by performing steps in a variety of solutions.

Default Value: Quantitation

Pattern Description: {Kinetics, EpitopeBinning, Quantitation, AssayDevelopment}

Programmatic Pattern: BLIApplicationsP

BioProbeType

Indicates the type of surface-functionalized fiber-optic probe to be used in this experiment. The probe surface functionalization may allow for direct binding to the analyte, or can be further functionalized with an immobilized secondary species, which would then interact with the solution phase analyte in a subsequent step.

Default Value: Model[Item, BLIProbe, ProA]

Pattern Description: An object of type or subtype Model[Item, BLIProbe] or Object[Item, BLIProbe]

Programmatic Pattern: ObjectP[{Model[Item, BLIProbe], Object[Item, BLIProbe]}]

NumberOfRepeats

The number of times that the assay will be repeated for each set of samples. All assay steps will be repeated with a new set of bio-probes unless a Regeneration option has been selected.

Default Value: Null

Pattern Description: Greater than or equal to 2 and less than or equal to 12 in increments of 1 or Null.

Programmatic Pattern: RangeP[2, 12, 1] | Null

AcquisitionRate

Indicates the number of recorded data points per second. A lower acquisition rate (2 Hz) will average more scans per data point, leading to better signal-to-noise ratios. A higher rate (10 Hz) will generates more data points per second, and is best suited for fast binding events which cause rapid changes in bio-layer thickness. The default value of 5 Hz balances data density with signal-to-noise ratio reduction and is suitable for most experiments.

Default Value: 5 hertz

Pattern Description: 2 hertz, 5 hertz, or 10 hertz.

Programmatic Pattern: 2*Hertz | 5*Hertz | 10*Hertz

PlateCover

Indicates if a plate cover should be included. This is recommended for assays which are expected to run for more than 4 hours in order to prevent evaporation.

Default Value: Automatic

Default Calculation: PlateCover default to True for assays over 4 hours in length.

Pattern Description: True or False.

Programmatic Pattern: BooleanP | Automatic

Temperature

The temperature of the 96 well plate in which the assay is run.

Default Value: Ambient

Pattern Description: Ambient or greater than or equal to 15 degrees Celsius and less than or equal to 40 degrees Celsius.

Programmatic Pattern: Ambient | RangeP[15*Celsius, 40*Celsius]

RecoupSample

Indicates if the SampleIn used for bio-layer interferometry measurement will be transferred back into the container that they were in prior to the measurement.

Default Value: False

Pattern Description: True or False.

Programmatic Pattern: BooleanP

Index Matches to: experiment samples

SaveAssayPlate

Indicates if the Assay Plate should be saved and stored or discarded after the assay is completed. Note that if both SaveAssayPlate and RecoupSample are True, input samples will be transferred out of the plate and the plate will be stored separately.

Default Value: False

Pattern Description: True or False.

Programmatic Pattern: BooleanP

DefaultBuffer

The primary buffer solution to be used as the default solution for baseline, equilibration, bio-probe rinsing, or dissociation steps. Note that all assay steps using this solution will occur in a single set of wells containing DefaultBuffer, with the exception of Dissociation steps. If multiple buffers are required, indicate the appropriate buffers in the assay specific options section, or by using the AssaySequencePrimitives.

Default Value: Model[Sample, StockSolution, BLI Kinetics Buffer, 1X]

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

ReuseSolution

Indicates groups of assay step types may share a set of wells if they are performed on an identical set of solutions. For example, selecting MeasureDissociation and MeasureBaseline will allow baseline and dissociation steps to occur steps in the same set of buffer wells. A single step, such as Wash, can also be selected to indicate that all Wash using identical solution should be performed in the same set of wells. This will increase the number of wells for available for sample measurement.

Default Value: {{MeasureBaseline, Wash, Equilibrate, MeasureDissociation, LoadSurface, ActivateSurface, Quench, Regenerate, Neutralize, Quantitate, MeasureAssociation}}

Pattern Description: List of one or more list of one or more Equilibrate, Wash, ActivateSurface, Quench, LoadSurface, Regenerate, Neutralize, MeasureBaseline, MeasureAssociation, MeasureDissociation, or Quantitate entries entries or Null.

Programmatic Pattern: {{BLIPrimitiveNameP..}..} | Null

Blank

The solution which does not contain the analyte to be use as a negative control. This solution can be used to provide a baseline for a given assay step, to account for non-specific binding of other solution species, or to verify the reproducibility of a given experiment.

Default Value: Automatic

Default Calculation: Blank will resolve to the same value as the DefaultBuffer when an experiment requires a negative control, and Null if it is not required for the assay.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

Standard

The solution, typically containing a concentration of analyte, to be used as a positive control. This can be used to account for baseline drift and changes in the bio-probe properties.

Default Value: Null

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

Assay Preparation

ProbeRackEquilibration

Indicates if the bio-probes used in the assay are equilibrated in ProbeRackEquilibrationBuffer solution while stored in the bio-probe rack, which holds bio-probes before and during the experiment. All bio-probes used in this experiment will remain immersed in the ProbRackEquilibrationBuffer until they are required for use in the assay.

Default Value: True

Pattern Description: True or False.

Programmatic Pattern: BooleanP

ProbeRackEquilibrationTime

The minimum amount of time that the bio-probes used in the assay are equilibrated in ProbeRackEquilibrationBuffer prior to use in the assay. All bio-probes used in this experiment will remain immersed in the ProbeEquilibrationBufferSolution until required for the assay.

Default Value: Automatic

Default Calculation: ProbeRackEquilibrationTime will default to 10 Minute if ProbeRackEquilibration is True.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 2 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 2*Hour] | Automatic) | Null

ProbeRackEquilibrationBuffer

Indicates the type of buffer used for ProbeRackEquilibration.

Default Value: Automatic

Default Calculation: ProbeRackEquilibrationBuffer defaults to DefaultBuffer when ProbeRackEquilibration is true.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

StartDelay

Dictates the amount of time that the assay plate is located in the instrument at the desired temperature prior to beginning the assay.

Default Value: Automatic

Default Calculation: StartDelay is set to 15 Minutes if the PlateTemperature is not Ambient. This allows the assay plate temperature to equilibrate.

Pattern Description: Greater than or equal to 0 minutes and less than or equal to 2 hours or Null.

Programmatic Pattern: (RangeP[0*Minute, 2*Hour] | Automatic) | Null

StartDelayShake

Indicates if the prepared-assay 96 well plate is shaken during the StartDelay time.

Default Value: Automatic

Default Calculation: StartDelayShake is set to True if the PlateTemperature is not Ambient.

Pattern Description: True or False or Null.

Programmatic Pattern: (BooleanP | Automatic) | Null

Equilibrate

Indicates if an assay step should be added to the beginning of the assay in which the bio-probes are equilibrated in the assay plate.

Default Value: Automatic

Default Calculation: Equilibrate defaults to True if ProbeRackEquilibration is False.

Pattern Description: True or False.

Programmatic Pattern: BooleanP | Automatic

EquilibrateTime

The amount of time that the bio-probes are immersed in EquilibrateBuffer as the first step in the assay.

Default Value: Automatic

Default Calculation: EquilibrateTime will default to 10 Minute if Equilibrate is True.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 2 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 2*Hour] | Automatic) | Null

EquilibrateBuffer

Indicates the type of buffer used for the Equilibrate step.

Default Value: Automatic

Default Calculation: EquilibrateBuffer defaults to DefaultBuffer when Equilibrate is True.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

EquilibrateShakeRate

Indicates the rate at which the assay 96 well plate is shaken during the Equilibrate step.

Default Value: Automatic

Default Calculation: EquilibrateShakeRate is set to 1000 RPM is Equilibrate is True.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

Post Experiment

StandardStorageCondition

Specifies non-default conditions under which the Standard should be stored after the protocol is completed. If left unset, the Standard will be stored according to the current StorageCondition.

Default Value: Null

Pattern Description: {AmbientStorage, Refrigerator, Freezer, DeepFreezer, CryogenicStorage, YeastIncubation, BacteriaIncubation, MammalianIncubation, TissueCultureCellsIncubation, MicrobialCellsIncubation, MicrobialCellsShakingIncubation, YeastCellsIncubation, YeastCellsShakingIncubation, ViralIncubation, AcceleratedTesting, IntermediateTesting, LongTermTesting, UVVisLightTesting} or Disposal or Null.

Programmatic Pattern: (SampleStorageTypeP | Disposal) | Null

LoadSolutionStorageCondition

Specifies non-default conditions under which the LoadSolution should be stored after the protocol is completed. If left unset, the LoadSolution will be stored according to the current StorageCondition.

Default Value: Null

Pattern Description: {AmbientStorage, Refrigerator, Freezer, DeepFreezer, CryogenicStorage, YeastIncubation, BacteriaIncubation, MammalianIncubation, TissueCultureCellsIncubation, MicrobialCellsIncubation, MicrobialCellsShakingIncubation, YeastCellsIncubation, YeastCellsShakingIncubation, ViralIncubation, AcceleratedTesting, IntermediateTesting, LongTermTesting, UVVisLightTesting} or Disposal or Null.

Programmatic Pattern: (SampleStorageTypeP | Disposal) | Null

QuantitationStandardStorageCondition

Specifies non-default conditions under which the QuantitationStandard should be stored after the protocol is completed. If left unset, the QuantitationStandard will be stored according to the current StorageCondition.

Default Value: Automatic

Default Calculation: If Standard is used as the QuantitationStandard, this will be set to StandardStorageCondition.

Pattern Description: {AmbientStorage, Refrigerator, Freezer, DeepFreezer, CryogenicStorage, YeastIncubation, BacteriaIncubation, MammalianIncubation, TissueCultureCellsIncubation, MicrobialCellsIncubation, MicrobialCellsShakingIncubation, YeastCellsIncubation, YeastCellsShakingIncubation, ViralIncubation, AcceleratedTesting, IntermediateTesting, LongTermTesting, UVVisLightTesting} or Disposal or Null.

Programmatic Pattern: ((SampleStorageTypeP | Disposal) | Automatic) | Null

QuantitationEnzymeSolutionStorageCondition

Specifies non-default conditions under which the QuantitationEnzymeSolution should be stored after the protocol is completed. If left unset, the QuantitationEnzymeSolution will be stored according to the current StorageCondition.

Default Value: Null

Pattern Description: {AmbientStorage, Refrigerator, Freezer, DeepFreezer, CryogenicStorage, YeastIncubation, BacteriaIncubation, MammalianIncubation, TissueCultureCellsIncubation, MicrobialCellsIncubation, MicrobialCellsShakingIncubation, YeastCellsIncubation, YeastCellsShakingIncubation, ViralIncubation, AcceleratedTesting, IntermediateTesting, LongTermTesting, UVVisLightTesting} or Disposal or Null.

Programmatic Pattern: (SampleStorageTypeP | Disposal) | Null

BinningAntigenStorageCondition

Specifies non-default conditions under which the BinningAntigen should be stored after the protocol is completed. If left unset, the BinningAntigen will be stored according to the current StorageCondition.

Default Value: Null

Pattern Description: {AmbientStorage, Refrigerator, Freezer, DeepFreezer, CryogenicStorage, YeastIncubation, BacteriaIncubation, MammalianIncubation, TissueCultureCellsIncubation, MicrobialCellsIncubation, MicrobialCellsShakingIncubation, YeastCellsIncubation, YeastCellsShakingIncubation, ViralIncubation, AcceleratedTesting, IntermediateTesting, LongTermTesting, UVVisLightTesting} or Disposal or Null.

Programmatic Pattern: (SampleStorageTypeP | Disposal) | Null

TestInteractionSolutionsStorageConditions

Specifies non-default conditions under which the TestInteractionSolutions should be stored after the protocol is completed. If left unset, the TestInteractionSolutions will be stored according to the current StorageCondition.

Default Value: Null

Pattern Description: {AmbientStorage, Refrigerator, Freezer, DeepFreezer, CryogenicStorage, YeastIncubation, BacteriaIncubation, MammalianIncubation, TissueCultureCellsIncubation, MicrobialCellsIncubation, MicrobialCellsShakingIncubation, YeastCellsIncubation, YeastCellsShakingIncubation, ViralIncubation, AcceleratedTesting, IntermediateTesting, LongTermTesting, UVVisLightTesting} or Disposal or Null.

Programmatic Pattern: (SampleStorageTypeP | Disposal) | Null

Index Matches to: experiment samples

TestLoadingSolutionsStorageConditions

Specifies non-default conditions under which the TestLoadingSolutions should be stored after the protocol is completed. If left unset, the TestLoadingSolutions will be stored according to the current StorageCondition.

Default Value: Null

Pattern Description: List of one or more {AmbientStorage, Refrigerator, Freezer, DeepFreezer, CryogenicStorage, YeastIncubation, BacteriaIncubation, MammalianIncubation, TissueCultureCellsIncubation, MicrobialCellsIncubation, MicrobialCellsShakingIncubation, YeastCellsIncubation, YeastCellsShakingIncubation, ViralIncubation, AcceleratedTesting, IntermediateTesting, LongTermTesting, UVVisLightTesting} or Disposal entries or Null.

Programmatic Pattern: {(SampleStorageTypeP | Disposal)..} | Null

SamplesInStorageCondition

The non-default conditions under which the SamplesIn of this experiment should be stored after the protocol is completed. If left unset, SamplesIn will be stored according to their current StorageCondition.

Default Value: Null

Pattern Description: {AmbientStorage, Refrigerator, Freezer, DeepFreezer, CryogenicStorage, YeastIncubation, BacteriaIncubation, MammalianIncubation, TissueCultureCellsIncubation, MicrobialCellsIncubation, MicrobialCellsShakingIncubation, YeastCellsIncubation, YeastCellsShakingIncubation, ViralIncubation, AcceleratedTesting, IntermediateTesting, LongTermTesting, UVVisLightTesting} or Disposal or Null.

Programmatic Pattern: (Alternatives[SampleStorageTypeP | Disposal]) | Null

Index Matches to: experiment samples

Dilution Preparation

DilutionMixVolume

The volume that is pipetted out and in of a given dilution to ensure homogeneous composition. This option also applies to PreMixSolution.

Default Value: 100 microliters

Pattern Description: Greater than or equal to 0 microliters and less than or equal to 2000 microliters or Null.

Programmatic Pattern: RangeP[0*Microliter, 2000*Microliter] | Null

DilutionNumberOfMixes

The number of pipette out and in cycles that is used to mix each dilution. This option also applies to PreMixSolution.

Default Value: 5

Pattern Description: Greater than or equal to 0 and less than or equal to 20 in increments of 1 or Null.

Programmatic Pattern: RangeP[0, 20, 1] | Null

DilutionMixRate

The rate at which the DilutionMixVolume is pipetted when mixing to ensure homogeneity. This option also applies to PreMixSolution.

Default Value: 50 microliters per second

Pattern Description: Greater than or equal to 0.5 microliters per second and less than or equal to 250 microliters per second or Null.

Programmatic Pattern: RangeP[0.5*(Microliter/Second), 250*(Microliter/Second)] | Null

Probe Regeneration

RegenerationType

Indicates the steps to be included when returning the bio-probe surface to a measurement-ready condition. Regenerate: Adds a step where the bio-probe is immersed in RegenerationSolution. Neutralize: The bio-probe is immersed in NeutralizationSolution after regeneration to neutralize the probe surface. Wash: Adds a washing step after Regeneration or Neutralization (if selected) in WashSolution to remove any residual solution. PreCondition: Performs the requested regeneration cycle prior to the first sample measurement to ensure all measurements are performed with identical assay steps.

Figure 3.1: Regeneration type available for ExperimentBioLayerInterferometry.

Default Value: None

Pattern Description: A selection of one or more of Regenerate, Neutralize, Wash, or PreCondition or None or Null.

Programmatic Pattern: (None | DuplicateFreeListableP[Regenerate | Neutralize | Wash | PreCondition]) | Null

RegenerationSolution

The solution used to remove residual analyte from the bio-probe surface. Regeneration with the appropriate solution will allow for reuse of a set of bio-probes for multiple measurements.

Default Value: Automatic

Default Calculation: RegenerationSolution defaults to Model[Sample, StockSolution, "2 M HCl"] if Regenerate is selected in RegenerationType

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

RegenerationCycles

Indicates the number of times bio-probe will be subjected to the selected Regenerate and Neutralize steps (prior to a Wash step, if selected).

Default Value: Automatic

Default Calculation: RegenerationCycles will be set to 3 if RegenerationParameters is not None. This will generally provide a good balance between complete bio-probe regeneration and experiment time.

Pattern Description: Greater than or equal to 0 and less than or equal to 10 in increments of 1 or Null.

Programmatic Pattern: (RangeP[0, 10, 1] | Automatic) | Null

RegenerationTime

The amount of time that the bio-probe is immersed in RegenerationSolution.

Default Value: Automatic

Default Calculation: RegenerationTime will be set to 5 Second if regeneration steps are included in the assay.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 minutes or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Minute] | Automatic) | Null

RegenerationShakeRate

The plate shake rate while the bio-probe is immersed in RegenerationSolution.

Default Value: Automatic

Default Calculation: RegenerationShakeRate will be set to 1000 RPM if regeneration steps are included in the assay.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

NeutralizationSolution

The solution that will be used to neutralize the bio-probe surface after regeneration. This solution prevents alteration of the bio-probe surface pH during the regeneration step.

Default Value: Automatic

Default Calculation: The NeutralizationSolution will be set to DefaultBuffer if neutralization steps are included in the assay.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

NeutralizationTime

The amount of time for which the bio-probe is immersed in NeutralizationSolution following Regeneration.

Default Value: Automatic

Default Calculation: NeutralizationTime will be set to 5 Second if neutralization steps are included in the assay.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 minutes or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Minute] | Automatic) | Null

NeutralizationShakeRate

The plate shake rate while the bio-probe is immersed in NeutralizationSolution following Regeneration.

Default Value: Automatic

Default Calculation: NeutralizationShakeRate will be set to 1000 RPM if neutralization steps are included in the assay.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

WashSolution

The solution in which the bio-probe is immersed after neutralization or regeneration, depending on the selection in RegenerationType. This solution prevents interference from the neutralization or regeneration solution.

Default Value: Automatic

Default Calculation: The WashSolution will be set to DefaultBuffer if Wash is selected in RegenerationType.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

WashTime

The amount of time for a step in which the bio-probe is immersed in WashSolution following Neutralization.

Default Value: Automatic

Default Calculation: The WashTime will be set to 5 Second if Wash is selected in RegenerationType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 minutes or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Minute] | Automatic) | Null

WashShakeRate

The shake rate for a step in which the bio-probe is immersed in WashSolution following Neutralization.

Default Value: Automatic

Default Calculation: WashShakeRate will be set to 1000 RPM if Wash is selected in RegenerationType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

Probe Loading

LoadingType

Indicates the steps used in the process of loading the immobilized species on the bio-probe. Select all that apply. Load: The bio-probe will be immersed in LoadingSolution prior to sample measurement steps. Activate: The bio-probe will be immersed in ActivationSolution prior to loading. Qunech: The bio-probe will be immersed in QuenchinSolution after loading.

Default Value: None

Pattern Description: A selection of one or more of Load, Activate, or Quench or None or Null.

Programmatic Pattern: (None | DuplicateFreeListableP[Load | Activate | Quench]) | Null

LoadSolution

The solution which contains a species that is to be immobilized on the bio-probe surface.

Default Value: Null

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

LoadTime

The amount of time for which the bio-probe surface with is functionalized with the immobilized species (in LoadSolution). This allows for modification of the probe surface such that it will be sensitive to the desired analyte. The LoadingTime will limit the step length in the event that a threshold condition is not met.

Default Value: Automatic

Default Calculation: LoadTime is set to 15 minutes if Load is selected in LoadingType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

LoadThresholdCriterion

Indicates if the threshold condition for change in bio-layer thickness which will trigger the completion of a Load step must be met by any single well, or all of the wells measured in the step. Wells containing a secondary solution such as a Blank or Standard are automatically excluded.

Default Value: Automatic

Pattern Description: All or Single or Null.

Programmatic Pattern: ((All | Single) | Automatic) | Null

LoadAbsoluteThreshold

The change in bio-layer thickness that will trigger the removal of the bio-probe from the LoadingSolution, and initiates the following assay step. This threshold sets the desired thickness of the loaded bio-layer, and can be used both to ensure sufficient loading and guard against over-saturation of the probe surface. Check Model[Instrument, BioLayerInterferometer] for limits on bio-layer thickness.

Default Value: Null

Pattern Description: Greater than 0 nanometers or Null.

Programmatic Pattern: GreaterP[0*Nanometer] | Null

LoadThresholdSlope

The rate of change in bio-layer thickness that will trigger the removal of the bio-probe from the LoadingSolution, and initiates the following assay step.

Default Value: Null

Pattern Description: Greater than 0 nanometers per minute or Null.

Programmatic Pattern: GreaterP[0*(Nanometer/Minute)] | Null

LoadThresholdSlopeDuration

The amount of time that a given rate of change in bio-layer thickness must be exceeded to trigger the removal of the bio-probe from the LoadingSolution, and initiate the following assay step.

Default Value: Null

Pattern Description: Greater than 0 seconds or Null.

Programmatic Pattern: GreaterP[0*Second] | Null

LoadShakeRate

The speed at which the plate is agitated while the bio-probe is immersed in LoadingSolution.

Default Value: Automatic

Default Calculation: LoadShakeRate is set to 1000 RPM if Load is selected in LoadingType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

ActivateSolution

Indicates the solution used to enhance the bio-probe surface capacity and affinity for the immobilized species. The bio-probe is immersed in this solution prior to exposure to the LoadingSolution.

Default Value: Null

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

ActivateTime

The amount of time for which the bio-probe is immersed in ActivationSolution prior to loading in LoadingSolution. Activation chemically modifies the probe surface, rendering it more receptive to the immobilized species.

Default Value: Automatic

Default Calculation: ActivateTime is set to 1 Minute if Activate is selected in LoadingType.

Pattern Description: Greater than or equal to 0 hours and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Hour, 20*Hour] | Automatic) | Null

ActivateShakeRate

The speed at which the plate is agitated while the bio-probe is immersed in ActivationSolution prior to loading in LoadingSolution.

Default Value: Automatic

Default Calculation: ActivateTime is set to 1000 RPM if Activate is selected in LoadingType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

QuenchSolution

The solution used to passivate un-reacted sites after loading the immobilized species by immersion in LoadingSolution. This will reduce the probability of non-selective binding between an analyte and the bio-probe surface.

Default Value: Null

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

QuenchTime

The amount of time for which the bio-probe is immersed in QuenchSolution after being functionalized with the immobilized species. This step passivates un-reacted sites and will reduce the probability of non-selective binding between an analyte and the bio-probe surface.

Default Value: Automatic

Default Calculation: QuenchTime is set to 1 Minute if Quench is selected in LoadingType.

Pattern Description: Greater than or equal to 0 hours and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Hour, 20*Hour] | Automatic) | Null

QuenchShakeRate

The speed at which the assay plate is shaken while the bio-probe is immersed in QuenchSolution after being functionalized with the immobilized species.

Default Value: Automatic

Default Calculation: QuenchShakeRate is set to 1000 RPM if Quench is selected in LoadingType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

Kinetics Assay

KineticsReferenceType

Indicates the type of non-sample solutions to be included. Select all that apply. A well containing the selected solution will be measured simultaneously during the association step. If multiple solutions are selected, one well for each solution will be included.

Figure 3.2: Kinetics reference type available for ExperimentBioLayerInterferometry.

Default Value: Null

Pattern Description: A selection of one or more of Blank or Standard or Null.

Programmatic Pattern: DuplicateFreeListableP[Blank | Standard] | Null

KineticsBaselineBuffer

The solution in which the bio-probes are immersed prior to performing the association step in a kinetics assay. This provides a baseline of the bio-layer thickness prior to analyte association.

Default Value: Automatic

Default Calculation: The KineticsBaselineBuffer is set to match the DefaultBuffer if it is informed and the ExperimentType is Kinetics.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

MeasureBaselineTime

The amount of time for which the bio-probe is immersed in KineticsBaselineBuffer directly prior to performing MeasureAssociation.

Default Value: Automatic

Default Calculation: MeasureBaselineTime is set to 30 Second if Kinetics is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

MeasureBaselineShakeRate

The speed at which the assay plate is shaken while the bio-probe is immersed in KineticsBaselineBuffer directly prior to performing MeasureAssociation.

Default Value: Automatic

Default Calculation: MeasureBaselineShakeRate is set to 1000 RPM if Kinetics is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

MeasureAssociationTime

The amount of time for which the bio-probe is immersed in the sample solution to measure analyte association.

Default Value: Automatic

Default Calculation: MeasureAssociationTime is set to 15 Minute if Kinetics is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

MeasureAssociationThresholdCriterion

Indicates if the threshold condition for change in bio-layer thickness which will trigger the completion of the Association step must be met by any single well, or all of the wells measured in the step. Wells containing a secondary solution such as a Blank or Standard are automatically excluded.

Default Value: Automatic

Default Calculation: MeasureAssociationThresholdCriterion is set to All if MeasureAssociationAbsoluteThreshold or MeasureAssociationThresholdSlope is specified.

Pattern Description: All or Single or Null.

Programmatic Pattern: ((All | Single) | Automatic) | Null

MeasureAssociationAbsoluteThreshold

The change in bio-layer thickness that will trigger the removal of the bio-probe from the sample solution, and initiate the following assay step. This threshold can be used to prevent excessively long association steps.

Default Value: Null

Pattern Description: Greater than 0 nanometers or Null.

Programmatic Pattern: GreaterP[0*Nanometer] | Null

MeasureAssociationThresholdSlope

The rate of change in bio-layer thickness that will trigger the removal of the bio-probe from the sample solution, and initiate the following assay step.

Default Value: Null

Pattern Description: Greater than 0 nanometers per minute or Null.

Programmatic Pattern: GreaterP[0*(Nanometer/Minute)] | Null

MeasureAssociationThresholdSlopeDuration

The amount of time that a given rate of change in bio-layer thickness must be exceeded to will trigger the removal of the bio-probe from the sample solution, and initiate the following assay step.

Default Value: Null

Pattern Description: Greater than 0 seconds or Null.

Programmatic Pattern: GreaterP[0*Second] | Null

MeasureAssociationShakeRate

The speed at which the assay plate is shaken while the bio-probe is immersed in the analyte solution.

Default Value: Automatic

Default Calculation: MeasureAssociationShakeRate is set to 1000 RPM if Kinetics is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

KineticsDissociationBuffer

The solution in which the dissociation step is performed in a Kinetics assay.

Default Value: Automatic

Default Calculation: The MeasureDissociationBuffer is set to match the KineticsBaselineBuffer if the ExperimentType is Kinetics.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

MeasureDissociationTime

The amount of time for which the bio-probe is immersed in KineticsDissociationBuffer to measure analyte dissociation.

Default Value: Automatic

Default Calculation: MeasureDissociationTime is set to 30 Minute if Kinetics is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

MeasureDissociationThresholdCriterion

Indicates if the threshold condition for change in bio-layer thickness which will trigger the completion of the dissociation step must be met by any single well, or all of the wells measured in the step. Wells containing a secondary solution such as a Blank or Standard are automatically excluded.

Default Value: Automatic

Default Calculation: MeasureDissociationThresholdCriterion is set to All if MeasureDissociationAbsoluteThreshold or MeasureDissociationThresholdSlope is specified.

Pattern Description: All or Single or Null.

Programmatic Pattern: ((All | Single) | Automatic) | Null

MeasureDissociationAbsoluteThreshold

The change in bio-layer thickness that will trigger the removal of the bio-probe from the sample solution, and initiate the following assay step. This threshold can prevent excessively long dissociation steps.

Default Value: Null

Pattern Description: Less than 0 nanometers or Null.

Programmatic Pattern: LessP[0*Nanometer] | Null

MeasureDissociationThresholdSlope

The rate of change in bio-layer thickness that will trigger the removal of the bio-probe from the sample solution, and initiate the following assay step.

Default Value: Null

Pattern Description: Greater than 0 nanometers per minute or Null.

Programmatic Pattern: GreaterP[0*(Nanometer/Minute)] | Null

MeasureDissociationThresholdSlopeDuration

The amount of time that a given rate of change in bio-layer thickness must be exceeded to will trigger the removal of the bio-probe from the sample solution, and initiate the following assay step.

Default Value: Null

Pattern Description: Greater than 0 seconds or Null.

Programmatic Pattern: GreaterP[0*Second] | Null

MeasureDissociationShakeRate

The speed at which the assay plate is shaken while the bio-probe is immersed in the MeasureDissociationBuffer solution.

Default Value: Automatic

Default Calculation: MeasureDissociationShakeRate is set to 1000 RPM if Kinetics is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

Kinetics Sample Preparation

KineticsSampleFixedDilutions

The collection of dilutions that will be performed on each sample to generate dilutions for association measurement. If the dilutions are prepared in 250 Microliter volumes, they will be performed on the assay plate. Otherwise, 250 Microliters of each dilution will be transferred to the assay plate. For Fixed Dilutions, the SampleAmount is the volume of the sample that will be mixed with the DiluentAmount of the Diluent to create a desired concentration.

Default Value: Automatic

Default Calculation: This is automatically set Null if Kinetics is not selected in ExperimentType. If Kinetics is selected it is automatically set to a create a series of 8 solutions which are 250 Microliters each, with concentrations evenly spaced between the concentration of the sample and 10 fold dilution. For example, given a 100 Micromolar sample, a series of dilutions with concentrations of 100, 89, 78, 66, 55, 44, 32, 21, 10 Micromolar would be generated.

Pattern Description: Fixed Dilution Factors or Fixed Dilution Volumes or Null.

Programmatic Pattern: (({{GreaterP[0*Microliter], GreaterEqualP[0*Microliter], _String}..} | {{GreaterEqualP[1], _String}..}) | Automatic) | Null

Index Matches to: experiment samples

KineticsSampleSerialDilutions

The collection of dilutions that will be performed on each sample to generate dilutions for association measurement. If the dilutions are prepared in 250 Microliter volumes, they will be performed on the assay plate. Otherwise, 250 Microliters of each dilution will be transferred to the assay plate. For Serial Dilutions, the TransferAmount is taken out of the sample and added to a second well with the DiluentAmount of the KineticsSampleDiluent. It is mixed, then the TransferAmount is taken out of that well to be added to a third well. This is repeated to make samples with the specified SolutionIDs.

Default Value: Null

Pattern Description: Serial Dilution Factors or Serial Dilution Volumes or Null.

Programmatic Pattern: (({GreaterP[0*Microliter], GreaterEqualP[0*Microliter], {_String..}} | {{GreaterEqualP[0*Microliter], GreaterEqualP[0*Microliter], _String}..}) | ({GreaterEqualP[2, 1], {_String..}} | {{GreaterEqualP[1, 1], _String}..})) | Null

Index Matches to: experiment samples

KineticsSampleDiluent

The solution that is used to dilute the samples to generate the solutions used in KineticsAssociation steps.

Default Value: Automatic

Default Calculation: If Kinetics has been selected in ExperimentType, KineticsSampleDiluent will default to DefaultBuffer.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

Index Matches to: experiment samples

Quantitation Assay

QuantitationParameters

A series of modifications on a basic quantitation experiment which are used inform the assay steps and plate layout. Select all that apply and populate options for the relevant solutions section. StandardCurve: Dilutions of user-specified solution (QuantitationStandard) are used to generate a calibration curve used to quantify analyte concentrations in samples. StandardWell: Simultaneously measure a well containing analyte of known concentration (QuantitationStandard) along with the unknown samples. BlankWell: Simultaneously measure a well of solution not containing the analyte (Blank solution) along with unknown samples. AmplifiedDetection: Performs quantitation measurement in DetectionSolution which amplifies the change in bio-layer thickness, yielding more sensitive detection. This solution is generally an antibody or other substrate that binds to the analyte on the probe surface, thereby increasing the bio-layer thickness CaptureAntibody: Includes a step in which the bio-probe is functionalized with a capture antibody by immersion in CaptureAntibodySolution. SecondaryAntibody: Includes a step in which the bio-probe is treated with another antibody (in SecondaryAntibodySolution) following the first treatment. EnzymeLinked: Exposes the bio-probe to EnzymeSolution for direct measurement, or prior to detection.

Figure 3.3: Various quantitation parameters available for ExperimentBioLayerInterferometry.

Default Value: Null

Pattern Description: A selection of one or more of StandardCurve, StandardWell, BlankWell, AmplifiedDetection, or EnzymeLinked or Null.

Programmatic Pattern: DuplicateFreeListableP[StandardCurve | StandardWell | BlankWell | AmplifiedDetection | EnzymeLinked] | Null

QuantitationStandard

Indicates a solution which is used to generate a standard curve for quantitation of the analyte concentration in the input samples.

Default Value: Automatic

Default Calculation: The QuantitionStandard will be set to the same value as the Standard if Quantitation is selected in ExperimentType and if the Standard has been user specified.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

QuantitationStandardWell

Indicates a solution which is measured in a single well in parallel with each quantitation step.

Default Value: Automatic

Default Calculation: The QuantitionStandardWell will be set to the same value as the QuantitationStandard if Quantitation is selected in ExperimentType and if the QuantitationStandard has been user specified.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

QuantitateTime

The amount of time for which the bio-probe is immersed in the sample solution to perform a quantitation measurement. This time will also apply to steps measuring the QuantitationStandard solutions, if requested in QuantititationParameters.

Default Value: Automatic

Default Calculation: QuantitateSampleMeasurementTime is set to 5 minutes if Quantitation is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

QuantitateShakeRate

The speed at which the assay plate is shaken while the bio-probe is immersed in the sample solution to perform a quantitation measurement. This will also apply to steps measuring the QuantitationStandard solutions, if requested in QuantititationParameters.

Default Value: Automatic

Default Calculation: QuantitateSampleMeasurementShakeRate is set to 1000 RPM if Quantitation is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

AmplifiedDetectionSolution

A solution containing a species which binds to the immobilized analyte on the bio-probe surface, thereby increasing the thickness of the bio-layer. This solution can improve the detection of an analyte in quantitation experiments, and is most commonly used when detecting enzymes.

Default Value: Null

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

AmplifiedDetectionTime

The amount of time for an amplified quantitation measurement step, in which the bio-probe is immersed in the AmplifiedDetectionSolution.

Default Value: Automatic

Default Calculation: AmplifiedDetectionTime is set to 5 minutes if AmplifiedDetection is selected in QuantitationParameters.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

AmplifiedDetectionShakeRate

The speed at which the assay plate is shaken for an amplified quantitation measurement step, in which the bio-probe is immersed in the DetectionSolution.

Default Value: Automatic

Default Calculation: AmplifiedDetectionShakeRate is set to 1000 RPM if AmplifiedDetection is selected in QuantitationParameters.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

QuantitationEnzymeSolution

Indicates a solution containing enzyme used to amplify quantitation results. The probe is immersed in QuantitationEnzymeSolution after immersion in the analyte solution.

Default Value: Null

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

QuantitationEnzymeBuffer

Indicates a solution used to rinse the probe between QuantitationEnzyme and Detection.

Default Value: Automatic

Default Calculation: QuantitationEnzymeBuffer will be set to DefaultBuffer if QuantitaionEnzyme is selected in QuantitationParameters.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

QuantitationEnzymeTime

The amount of time which the bio-probe is immersed in an enzyme solution (QuantitationEnzymeSolution). This step is performed after bio-probe immersion in the sample solutions.

Default Value: Automatic

Default Calculation: QuantitationEnzymeTime is set to 5 minutes if QuantitaionEnzyme is selected in QuantitationParameters.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

QuantitationEnzymeShakeRate

The speed at which the assay plate is shaken while the bio-probe is immersed in an enzyme solution (QuantitationEnzymeSolution). This step is performed after bio-probe immersion in the sample solutions.

Default Value: Automatic

Default Calculation: QuantitationEnzymeShakeRate is set to 1000 RPM if QuantitaionEnzyme is selected in QuantitationParameters.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

Quantitation Standard Preparation

QuantitationStandardFixedDilutions

The collection of dilutions that will be performed on the QuantitationStandard to generate a standard curve for a Quantitation experiment. If the dilutions are prepared in 250 Microliter volumes, they will be performed on the assay plate. Otherwise, 250 Microliters of each dilution will be transferred to the assay plate. For Fixed Dilution Volumes, the SampleAmount is the volume of the sample that will be mixed with the DiluentAmount of the Diluent to create a desired concentration. For Fixed Dilution Factors, an appropriate amount of sample will mixed with diluent to achieve a solution with the requested volume and concentration. The SolutionIDs are used to indicate a unique temporary name for each dilution that is referred to in the protocol object.

Default Value: Automatic

Default Calculation: This is automatically set to Null if QuantitationStandard is set to Null. In all other cases it is automatically set to a create a series of dilutions of the QuantitationStandard using dilution factors of 2, 4, 8, 16, 32, 64, and 128 and diluting with QuantiationDiluent.

Pattern Description: Fixed Dilution Factors or Fixed Dilution Volumes or Null.

Programmatic Pattern: (({{GreaterP[0*Microliter], GreaterP[0*Microliter], _String}..} | {{GreaterEqualP[1], _String}..}) | Automatic) | Null

QuantitationStandardSerialDilutions

The collection of dilutions that will be performed on the QuantitationStandard to generate a standard curve for a Quantitation experiment. For volume based Serial Dilutions, the TransferAmount is taken out of the QuantitationStandard and added to a second well with the DiluentAmount of the QuantitationStandardDiluent. It is mixed, then the TransferAmount is taken out of that well to be added to a third well. This is repeated to the solutions labeled by SolutionIDs. For dilution factor based Serial Dilutions, the appropriate amount of solution will be added to a diluent to achieve the solutions with desired dilution factor and final volumes of > 250 uL. The SolutionIDs are used to indicate a unique temporary name for each dilution that is referred to in the protocol object.

Default Value: Null

Pattern Description: Serial Dilution Factors or Serial Dilution Volumes or Null.

Programmatic Pattern: (({GreaterP[0*Microliter], GreaterEqualP[0*Microliter], {_String..}} | {{GreaterEqualP[0*Microliter], GreaterEqualP[0*Microliter], _String}..}) | ({GreaterEqualP[2, 1], {_String..}} | {{GreaterEqualP[1, 1], _String}..})) | Null

QuantitationStandardDiluent

The solution that is used to dilute the QuantitationStandard to generate the solutions used in the quantitation standard curve.

Default Value: Automatic

Default Calculation: If the a dilution series has been specified, QuantitationStandardDiluent will default to DefaultBuffer.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

Epitope Binning Assay

BinningType

Indicates the assay configuration for EpitopeBinning. Sandwich: The first antibody is bound to the bio-probe surface. The surface is first exposed to the target antigen (BinningAntigen), then to solutions of competing antibodies. Tandem: The target antigen species is immobilized on the bio-probe surface. The surface is then exposed to a pair of competing antibodies sequentially. Premix: An antibody is bound to the bio-probe surface. The bio-probe is then exposed to a premixed solution of antigen and competing antibody.

Figure 3.4: Various binning types available for ExperimentBioLayerInterferometry.

Default Value: Automatic

Default Calculation: If EpitopeBinning is selected in ExperimentType, BinningType will default to Sandwich, otherwise it will default to Null.

Pattern Description: Sandwich, PreMix, or Tandem or Null.

Programmatic Pattern: ((Sandwich | PreMix | Tandem) | Automatic) | Null

BinningControlWell

During the Antibody loading step, one well of Blank solution will be included. This will reduce the maximum number of antibodies from 8 to 7.

Default Value: Automatic

Default Calculation: BinningControlWell defaults to True if EpitopeBinning is selected in ExperimentType, otherwise it will default to Null.

Pattern Description: True or False or Null.

Programmatic Pattern: (BooleanP | Automatic) | Null

LoadAntibodyTime

For Sandwich-type assays: The amount of time for which the bio-probe surface with is saturated with bound antibody. For Tandem-type assays: The amount of time for which the antigen coated bio-probe surface with is immersed in the first antibody solution.

Default Value: Automatic

Default Calculation: LoadAntibodyTime is set to 10 minutes if EpitopeBinning is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

LoadAntibodyThresholdCriterion

Indicates if the threshold condition for change in bio-layer thickness which will trigger the completion of an assay step must be met by any single well, or all of the wells measured in the step. Wells containing a secondary solution such as a Blank or Standard are automatically excluded.

Default Value: Automatic

Default Calculation: LoadAntibodyThresholdCriterion is set to All if LoadAntibodyAbsoluteThreshold or LoadAntibodyThresholdSlope is specified.

Pattern Description: All or Single or Null.

Programmatic Pattern: ((All | Single) | Automatic) | Null

LoadAntibodyAbsoluteThreshold

The change in bio-layer thickness that will trigger the removal of the bio-probe from the antibody solution, and initiate the following assay step. This threshold can be used to ensure an appropriate amount of antibody association, and prevent over-saturation of the probe surface.

Default Value: Null

Pattern Description: Greater than 0 nanometers or Null.

Programmatic Pattern: GreaterP[0*Nanometer] | Null

LoadAntibodyThresholdSlope

The rate of change in bio-layer thickness that will trigger the removal of the bio-probe from the antibody solution, and initiate the following assay step.

Default Value: Null

Pattern Description: Greater than 0 nanometers per minute or Null.

Programmatic Pattern: GreaterP[0*(Nanometer/Minute)] | Null

LoadAntibodyThresholdSlopeDuration

The amount of time that a given rate of change in bio-layer thickness must be exceeded to will trigger the removal of the bio-probe from the antibody solution, and initiate the following assay step.

Default Value: Null

Pattern Description: Greater than 0 seconds or Null.

Programmatic Pattern: GreaterP[0*Second] | Null

LoadAntibodyShakeRate

For Sandwich-type assays: The speed at which the assay plate is shaken while the bio-probe surface with is saturated with bound antibody. For Tandem-type assays: The speed at which the assay plate is shaken while the antigen coated bio-probe surface with is immersed in the first antibody solution.

Default Value: Automatic

Default Calculation: LoadAntibodyShakeRate is set to 1000 RPM if EpitopeBinning is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

BinningQuenchSolution

Indicates a solution used to quench unreacted sites on the probe surface after antibody loading. Immersion of the bio-probe in this solution can help prevent non-selective binding in subsequent assay steps.

Default Value: Null

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

BinningQuenchTime

The amount of time for which the bio-probe is immersed in BinningQuenchSolution, which blocks unreacted sites. This option will override any assignment made in Loading Information.

Default Value: Automatic

Default Calculation: BinningQuenchTime is set to 5 minutes if EpitopeBinning is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

BinningQuenchShakeRate

The speed at which the assay plate is shaken while the bio-probe is immersed in BinningQuenchSolution, which blocks unreacted sites. This option will override any assignment made in Loading Information.

Default Value: Automatic

Default Calculation: BinningQuenchShakeRate is set to 1000 RPM if EpitopeBinning is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

BinningAntigen

Indicates a solution used in the Tandem and Sandwich type assays to populate the bio-probe surface with the target antigen.

Default Value: Null

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

LoadAntigenTime

For Sandwich-type assays: The amount of time while the antibody functionalized bio-probe surface is exposed to BinningAntigen. For Tandem-type assays: The amount of time while the bio-probe surface is saturated with antigen in BinningAntigen solution.

Default Value: Automatic

Default Calculation: LoadAntigenTime is set to 10 minutes if EpitopeBinning is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

LoadAntigenThresholdCriterion

Indicates if the threshold condition for change in bio-layer thickness which will trigger the completion of an antigen association step must be met by any single well, or all of the wells measured in the step. Wells containing a secondary solution such as a Blank or Standard are automatically excluded.

Default Value: Automatic

Default Calculation: LoadAntigenThresholdCriterion is set to All if LoadAntigenAbsoluteThreshold or LoadAntigenThresholdSlope is specified.

Pattern Description: All or Single or Null.

Programmatic Pattern: ((All | Single) | Automatic) | Null

LoadAntigenAbsoluteThreshold

The change in bio-layer thickness that will trigger the removal of the bio-probe from the antigen solution, and initiate the next assay step. This threshold can ensure an appropriate amount of antigen association, preventing oversaturation of the probe surface.

Default Value: Null

Pattern Description: Greater than 0 nanometers or Null.

Programmatic Pattern: GreaterP[0*Nanometer] | Null

LoadAntigenThresholdSlope

The rate of change in bio-layer thickness that will trigger the removal of the bio-probe from the antigen solution, and initiate the next assay step.

Default Value: Null

Pattern Description: Greater than 0 nanometers per minute or Null.

Programmatic Pattern: GreaterP[0*(Nanometer/Minute)] | Null

LoadAntigenThresholdSlopeDuration

The amount of time that a given rate of change in bio-layer thickness must be exceeded to will trigger the removal of the bio-probe from the antibody solution, and initiate the next assay step.

Default Value: Null

Pattern Description: Greater than 0 seconds or Null.

Programmatic Pattern: GreaterP[0*Second] | Null

LoadAntigenShakeRate

For Sandwich-type assays: The speed at which the assay plate is shaken for a step in which the antibody functionalized bio-probe surface is exposed to BinningAntigen. For Tandem-type assays: The speed at which the assay plate is shaken for a step in which the bio-probe surface is saturated with antigen in BinningAntigen.

Default Value: Automatic

Default Calculation: LoadAntigenShakeRate is set to 1000 RPM if EpitopeBinning is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

CompetitionBaselineBuffer

The solution in which the bio-probe is immersed prior to performing the competition step of an EpitopeBinning assay.

Default Value: Automatic

Default Calculation: The CompetitionBaselineBuffer is set to match the DefaultBuffer if the ExperimentType is EpitopeBinning.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

CompetitionBaselineTime

The amount of time while the bio-probe is immersed in BinningBaselineBuffer solution prior to performing the competition step of a EpitopeBinning assay.

Default Value: Automatic

Default Calculation: CompetitionBaselineTime is set to 30 seconds if EpitopeBinning is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

CompetitionBaselineShakeRate

The speed at which the assay plate is shaken while the bio-probe is immersed in CompetitionBaselineBuffer solution prior to performing the competition step of a EpitopeBinning assay.

Default Value: Automatic

Default Calculation: CompetitionBaselineShakeRate is set to 1000 RPM if EpitopeBinning is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

CompetitionTime

The amount of time while the bio-probe is immersed in a competing antibody (sample) or premixed antibody/antigen solution to observe competitive binding.

Default Value: Automatic

Default Calculation: CompetitionTime is set to 10 minutes if EpitopeBinning is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

CompetitionShakeRate

The speed at which the assay plate is shaken while the bio-probe is immersed in a competing antibody (sample) or premixed antibody/antigen solution to observe competitive binding.

Default Value: Automatic

Default Calculation: CompetitionShakeRate is set to 1000 RPM if EpitopeBinning is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

CompetitionThresholdCriterion

Indicates if the threshold condition for change in bio-layer thickness which will trigger the completion of an assay step must be met by any single well, or all of the wells measured in the step. Wells containing a secondary solution such as a Blank or Standard are automatically excluded.

Default Value: Automatic

Default Calculation: CompetitionThresholdCriterion is set to Single if CompetitionAbsoluteThreshold or CompetitionThresholdSlope is specified.

Pattern Description: All or Single or Null.

Programmatic Pattern: ((All | Single) | Automatic) | Null

CompetitionAbsoluteThreshold

The change in bio-layer thickness that will trigger the removal of the bio-probe from the antibody solution, and initiate the following assay step. This threshold can be used prevent excessively long step times.

Default Value: Null

Pattern Description: Greater than 0 nanometers or Null.

Programmatic Pattern: GreaterP[0*Nanometer] | Null

CompetitionThresholdSlope

The rate of change in bio-layer thickness that will trigger the removal of the bio-probe from the sample solution, and initiates the following assay step. This can be used to ensure that the probe surface reaches an equilibrium condition.

Default Value: Null

Pattern Description: Greater than 0 nanometers per minute or Null.

Programmatic Pattern: GreaterP[0*(Nanometer/Minute)] | Null

CompetitionThresholdSlopeDuration

The amount of time that a given rate of change in bio-layer thickness must be exceeded to will trigger the removal of the bio-probe from the sample solution, and initiates the following assay step.

Default Value: Null

Pattern Description: Greater than 0 seconds or Null.

Programmatic Pattern: GreaterP[0*Second] | Null

PreMixSolutions

The mixture of antibody solutions (the sample solutions) and antigen solution (BinningAntigen) which compose the PreMixSolutions. The solutions can be combined with PreMixDiluent to adjust the final concentration of the PreMixSolutions.

Default Value: Automatic

Default Calculation: This is automatically set Null if PreMix is not selected in BinningExperimentType. If PreMix is selected it is automatically set to mix 100 Microliters of the sample solution with 100 Microliters of the BinningAntigen.

Pattern Description: {SampleAmount, BinningAntigenAmount, PreMixDiluentAmount, SolutionIDs} or Null.

Programmatic Pattern: ({GreaterEqualP[0*Microliter], GreaterEqualP[0*Microliter], GreaterEqualP[0*Microliter], _String} | Automatic) | Null

Index Matches to: experiment samples

PreMixDiluent

The solution that is used to dilute the PreMixSolutions.

Default Value: Automatic

Default Calculation: If PreMix has been selected in BinningType, PreMixDiluent will be set to DefaultBuffer.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

Assay Development

DevelopmentType

Indicates which step or solution is being optimized or investigated. All assays will include an association step (in the input sample solution) and a dissociation step (in DefaultBuffer or TestBufferSolutions). ScreenLoading: Find the best loading condition or immobilized species from a list of TestLoadingSolutions. ScreenInteraction: Test interaction of pairs of immobilized and solution species using the TestInteractionSolutions. These solutions will be used in the load step, and are index matched to the sample input. ScreenBuffer: Perform measurements using a list of TestBufferSolutions. ScreenRegeneration: Perform regeneration using a series of TestRegenerationSolutions. ScreenActivation: Test activation conditions prior to a LoadSurface step, using different activation TestActivationSolutions. ScreenDetectionLimit: Perform identical measurements on increasingly dilute solutions to determine the detection limit for a given analyte.

Default Value: Automatic

Default Calculation: If AssayDevelopment is selected in ExperimentType, the DevelopmentType is set to ScreenDetectionLimit.

Pattern Description: ScreenLoading, ScreenInteraction, ScreenBuffer, ScreenRegeneration, ScreenActivation, or ScreenDetectionLimit or Null.

Programmatic Pattern: ((ScreenLoading | ScreenInteraction | ScreenBuffer | ScreenRegeneration | ScreenActivation | ScreenDetectionLimit) | Automatic) | Null

DevelopmentReferenceWell

Indicates if a well containing Blank, Standard or both should be measured in parallel with the samples in the developmentAssociation step.

Default Value: Null

Pattern Description: A selection of one or more of Blank or Standard or Null.

Programmatic Pattern: DuplicateFreeListableP[Blank | Standard] | Null

DevelopmentBaselineTime

The amount of time a bio-probe is immersed in buffer (DefaultBuffer or TestBufferSolutions) solution to record a baseline.

Default Value: Automatic

Default Calculation: DevelopmentBaselineTime is set to 30 seconds if AssayDevelopment is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

DevelopmentBaselineShakeRate

The speed at which the assay plate is shaken while a bio-probe is immersed in buffer (DefaultBuffer or TestBufferSolutions) solution to record a baseline.

Default Value: Automatic

Default Calculation: DevelopmentBaselineShakeRate is set to 1000 RPM if AssayDevelopment is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

DevelopmentAssociationTime

The amount of time which the bio-probe is immersed in sample solution to measure analyte association.

Default Value: Automatic

Default Calculation: AssayDevelopmentAssociationTime is set to 5 minutes if AssayDevelopment is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

DevelopmentAssociationThresholdCriterion

Indicates if the threshold condition for change in bio-layer thickness which will trigger the completion of an association step must be met by any single well, or all of the wells measured in the step. Wells containing a secondary solution such as a Blank or Standard are automatically excluded.

Default Value: Automatic

Default Calculation: DevelopmentAssociationThresholdCriterion is set to All if DevelopmentAssociationAbsoluteThreshold or DevelopmentAssociationThresholdSlope is specified.

Pattern Description: All or Single or Null.

Programmatic Pattern: ((All | Single) | Automatic) | Null

DevelopmentAssociationAbsoluteThreshold

The change in bio-layer thickness that will trigger the removal of the bio-probe from the sample solution, and initiate the next assay step. This threshold can prevent excessively long association steps.

Default Value: Null

Pattern Description: Greater than 0 nanometers or Null.

Programmatic Pattern: GreaterP[0*Nanometer] | Null

DevelopmentAssociationThresholdSlope

The rate of change in bio-layer thickness that will trigger the removal of the bio-probe from the sample solution, and initiate the next assay step.

Default Value: Null

Pattern Description: Greater than 0 nanometers per minute or Null.

Programmatic Pattern: GreaterP[0*(Nanometer/Minute)] | Null

DevelopmentAssociationThresholdSlopeDuration

The amount of time that a given rate of change in bio-layer thickness must be exceeded to will trigger the removal of the bio-probe from the sample solution, and initiate the next assay step.

Default Value: Null

Pattern Description: Greater than 0 seconds or Null.

Programmatic Pattern: GreaterP[0*Second] | Null

DevelopmentAssociationShakeRate

The speed at which the assay plate is shaken while the bio-probe is immersed in sample solution to measure analyte association.

Default Value: Automatic

Default Calculation: AssayDevelopmentAssociationShakeRate is set to 1000 RPM if AssayDevelopment is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

DevelopmentDissociationTime

The amount of time for which the bio-probe is immersed in DefaultBuffer or TestBufferSolutions during analyte dissociation.

Default Value: Automatic

Default Calculation: AssayDevelopmentDissociationTime is set to 30 minutes if AssayDevelopment is selected as the ExperimentType.

Pattern Description: Greater than or equal to 0 seconds and less than or equal to 20 hours or Null.

Programmatic Pattern: (RangeP[0*Second, 20*Hour] | Automatic) | Null

DevelopmentDissociationThresholdCriterion

Indicates if the threshold condition for change in bio-layer thickness which will trigger the completion of an dissociation step must be met by any single well, or all of the wells measured in the step. Wells containing a secondary solution such as a Blank or Control are automatically excluded.

Default Value: Automatic

Default Calculation: DevelopmentDissociationThresholdCriterion is set to All if DevelopmentDissociationAbsoluteThreshold or DevelopmentDissociationThresholdSlope is specified.

Pattern Description: All or Single or Null.

Programmatic Pattern: ((All | Single) | Automatic) | Null

DevelopmentDissociationAbsoluteThreshold

The change in bio-layer thickness that will trigger the removal of the bio-probe from the buffer solution, and initiate the next assay step. This threshold can be used to prevent excessively long dissociation steps.

Default Value: Null

Pattern Description: Greater than 0 nanometers or Null.

Programmatic Pattern: GreaterP[0*Nanometer] | Null

DevelopmentDissociationThresholdSlope

The rate of change in bio-layer thickness that will trigger the removal of the bio-probe from the buffer solution, and initiate the next assay step.

Default Value: Null

Pattern Description: Greater than 0 nanometers per minute or Null.

Programmatic Pattern: GreaterP[0*(Nanometer/Minute)] | Null

DevelopmentDissociationThresholdSlopeDuration

The amount of time that a given rate of change in bio-layer thickness must be exceeded to will trigger the removal of the bio-probe from the buffer solution, and initiate the next assay step.

Default Value: Null

Pattern Description: Greater than 0 seconds or Null.

Programmatic Pattern: GreaterP[0*Second] | Null

DevelopmentDissociationShakeRate

The speed at which the assay plate is shaken while the bio-probe is immersed in DefaultBuffer or TestBufferSolutions during analyte dissociation.

Default Value: Automatic

Default Calculation: AssayDevelopmentDissociationShakeRate is set to 1000 RPM if AssayDevelopment is selected as the ExperimentType.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 1500 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 1500*RPM] | Automatic) | Null

Assay Development Solutions

DetectionLimitSerialDilutions

The collection of dilutions that will be performed on each sample to generate dilutions to determine the limit of detection for one or more analytes. If the dilutions are prepared in 250 Microliter volumes, they will be performed on the assay plate. Otherwise, 250 Microliters of each dilution will be transferred to the assay plate. For Serial Dilutions, the TransferAmount is taken out of the sample and added to a second well with the DiluentAmount of the DetectionLimitDiluent. It is mixed, then the TransferAmount is taken out of that well to be added to a third well. This is repeated to make each of the solutions labeled by SolutionIDs.

Default Value: Automatic

Default Calculation: This is automatically set Null if DetectionLimit is not selected in DevelopmentType. If DetectionLimit is selected it is automatically set to a create a series of 6 solutions which are 250 Microliters each, using serial dilution of 50 Microliters of sample into 250 Microliters of DetectionLimitDiluent.

Pattern Description: Serial Dilution Factors or Serial Dilution Volumes or Null.

Programmatic Pattern: ((({GreaterP[0*Microliter], GreaterEqualP[0*Microliter], {_String..}} | {{GreaterEqualP[0*Microliter], GreaterEqualP[0*Microliter], _String}..}) | ({GreaterEqualP[2, 1], {_String..}} | {{GreaterEqualP[1, 1], _String}..})) | Automatic) | Null

Index Matches to: experiment samples

DetectionLimitFixedDilutions

The collection of dilutions that will be performed on each sample to generate dilutions to determine the limit of detection for one or more analytes. If the dilutions are prepared in 250 Microliter volumes, they will be performed on the assay plate. Otherwise, 250 Microliters of each dilution will be transferred to the assay plate. For Fixed Dilution Volumes, the SampleAmount is the volume of the sample that will be mixed with the DiluentAmount of the DetectionLimitDiluent to create a desired concentration. For Fixed Dilution Factors, the appropriate amount of sample volume is mixed with diluent to create a solution with the desired dilution factor and volume.

Default Value: Null

Pattern Description: Fixed Dilution Factors or Fixed Dilution Volumes or Null.

Programmatic Pattern: ({{GreaterP[0*Microliter], GreaterP[0*Microliter], _String}..} | {{GreaterEqualP[1], _String}..}) | Null

Index Matches to: experiment samples

DetectionLimitDiluent

The solution that is used to dilute the samples to generate a set of sample which can be used to establish a limit of detection for a given bio-probe/analyte pairing.

Default Value: Automatic

Default Calculation: If DetectionLimit has been selected in DevelopmentType, DetectionLimitDiluent will default to DefaultBuffer.

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

Index Matches to: experiment samples

TestInteractionSolutions

The list of solutions which are used to load the bio-probe surface for pair-wise interaction screening. This list is required if ScreenInteraction is selected.

Default Value: Null

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

Index Matches to: experiment samples

TestBufferSolutions

The list of solutions to be used as buffers. This list is required if ScreenBuffer is selected.

Default Value: Null

Pattern Description: List of one or more an object of type or subtype Object[Sample] or Model[Sample] or a prepared sample entries or Null.

Programmatic Pattern: {(ObjectP[{Object[Sample], Model[Sample]}] | _String)..} | Null

TestRegenerationSolutions

The list of solutions to be used to return the probe to a measurement-ready condition. This list is required if ScreenRegeneration is selected.

Default Value: Null

Pattern Description: List of one or more an object of type or subtype Object[Sample] or Model[Sample] or a prepared sample entries or Null.

Programmatic Pattern: {(ObjectP[{Object[Sample], Model[Sample]}] | _String)..} | Null

TestLoadingSolutions

The list of solutions in which the bio-probe will be immersed to load the immobilized species. This list is required if ScreenLoading is selected.

Default Value: Null

Pattern Description: List of one or more an object of type or subtype Object[Sample] or Model[Sample] or a prepared sample entries or Null.

Programmatic Pattern: {(ObjectP[{Object[Sample], Model[Sample]}] | _String)..} | Null

TestActivationSolutions

The list of solutions in which the bio-probe will be immersed in prior to loading the immobilized species. This list is required if ScreenActivation is selected.

Default Value: Null

Pattern Description: List of one or more an object of type or subtype Object[Sample] or Model[Sample] or a prepared sample entries or Null.

Programmatic Pattern: {(ObjectP[{Object[Sample], Model[Sample]}] | _String)..} | Null

Assay Primitives

AssaySequencePrimitives

The sequence of assay steps which will apply to each input sample. This sequence will be repeated the necessary number of times to perform the requested experiments, which the exception of Activation/Loading/Quench sequences, which will not be repeated if Regenerate steps are included. Analytes/Solution/Buffers: The solution(s) required for the assay step. Controls: Solutions (usually a blank or control) which will occupy one well in the assay plate, and are measured in parallel with the primary solution. Time: The amount of time for which the probe is immersed in the solution, if a threshold condition is not met, this time will limit the step length. Threshold: Select between Absolute (based on the total change in bio-layer thickness) and Slope (based on the rate of change in the bio-layer thickness). AbsoluteThreshold: The change in bio-layer thickness which will trigger the next assay step to begin. This can be used to ensure an appropriate amount of association to the probe surface. ThresholdType: Indicates if the threshold conditions must be met by any single well or all of the wells containing the primary solution. ThresholdSlope: The change in bio-layer thickness over time. ThresholdSlopeDuration: The amount of time for which the change in bio layer thickness over time must be less than that the ThresholdSlope to trigger the next step. ShakeRate: The rate at which the assay plate is shaken during this step.

Default Value: Automatic

Default Calculation: The order, type, and contents of the primitives are determined from the options. For example, setting options ExperimentType -> Kinetics, and LoadingType -> Loading would generate AssaySequencePrimitives of {Equilibrate,Load,Baseline,MeasureAssociation,MeasureDissociation}, with the solution, step times, thresholds, and shake-rate as specified in the options.

Pattern Description: List of one or more a primitive with head MeasureBaseline, Equilibrate, ActivateSurface, LoadSurface, Quantitate, Quench, Regenerate, Neutralize, Wash, MeasureAssociation, or MeasureDissociation entries.

Programmatic Pattern: {ValidBLIPrimitiveP..} | Automatic

ExpandedAssaySequencePrimitives

The exact sequence of assay steps which will be performed for this bio-layer interferometry experiment, grouped by steps that will be performed with the same probe.

Default Value: Automatic

Default Calculation: The ExpandedAssaySequencePrimitives are based on the AssaySequencePrimitives as defined directly by the user or by user input options.

Pattern Description: List of one or more list of one or more a primitive with head MeasureBaseline, Equilibrate, ActivateSurface, LoadSurface, Quantitate, Quench, Regenerate, Neutralize, Wash, MeasureAssociation, or MeasureDissociation entries entries.

Programmatic Pattern: {{ValidBLIPrimitiveP..}..} | Automatic

RepeatedSequence

The sequence of steps that are repeated by each bio-probe when regeneration is requested. For example, if the AssaySequencePrimitives -> {Load, Quantitate, Regenerate}, RepeatedSequence -> {Load, Quantitate, Regenerate} would return the probe to its original state, while RepeatedSequence -> {Quantitate, Regenerate} would return the surface as functionalized in the Load step.

Default Value: Automatic

Default Calculation: RepeatedSequence resolves to the subset of AssaySequencePrimitives names which occur for each sample following the initial measurement. RepeatedSequence resolves to Null unless there is a Regenerate step in AssaySequencePrimitives

Pattern Description: List of one or more {Equilibrate, Wash, ActivateSurface, Quench, LoadSurface, Regenerate, Neutralize, MeasureBaseline, MeasureAssociation, MeasureDissociation, Quantitate} entries or Null.

Programmatic Pattern: ({BLIPrimitiveNameP..} | Automatic) | Null



Sample Prep Options

Sample Preparation

PreparatoryUnitOperations

Specifies a sequence of transferring, aliquoting, consolidating, or mixing of new or existing samples before the main experiment. These prepared samples can be used in the main experiment by referencing their defined name. For more information, please reference the documentation for ExperimentSampleManipulation.

Default Value: Null

Pattern Description: List of one or more unit Operation ManualSamplePreparation or RoboticSamplePreparation or unit Operation must match SamplePreparationP entries or Null.

Programmatic Pattern: {((ManualSamplePreparationMethodP | RoboticSamplePreparationMethodP) | SamplePreparationP)..} | Null

PreparatoryPrimitives

Specifies a sequence of transferring, aliquoting, consolidating, or mixing of new or existing samples before the main experiment. These prepared samples can be used in the main experiment by referencing their defined name. For more information, please reference the documentation for ExperimentSampleManipulation.

Default Value: Null

Pattern Description: List of one or more a primitive with head Define, Transfer, Mix, Aliquot, Consolidation, FillToVolume, Incubate, Filter, Wait, Centrifuge, or Resuspend entries or Null.

Programmatic Pattern: {SampleManipulationP..} | Null

Preparatory Incubation

Incubate

Indicates if the SamplesIn should be incubated at a fixed temperature prior to starting the experiment or any aliquoting. Sample Preparation occurs in the order of Incubation, Centrifugation, Filtration, and then Aliquoting (if specified).

Default Value: Automatic

Default Calculation: Resolves to True if any of the corresponding Incubation options are set. Otherwise, resolves to False.

Pattern Description: True or False.

Programmatic Pattern: BooleanP | Automatic

Index Matches to: experiment samples

IncubationTemperature

Temperature at which the SamplesIn should be incubated for the duration of the IncubationTime prior to starting the experiment.

Default Value: Automatic

Pattern Description: Ambient or greater than or equal to -20 degrees Celsius and less than or equal to 500 degrees Celsius or Null.

Programmatic Pattern: ((Ambient | RangeP[$MinIncubationTemperature, $MaxIncubationTemperature]) | Automatic) | Null

Index Matches to: experiment samples

IncubationTime

Duration for which SamplesIn should be incubated at the IncubationTemperature, prior to starting the experiment.

Default Value: Automatic

Pattern Description: Greater than or equal to 1 minute and less than or equal to 72 hours or Null.

Programmatic Pattern: (RangeP[1*Minute, $MaxExperimentTime] | Automatic) | Null

Index Matches to: experiment samples

Mix

Indicates if this sample should be mixed while incubated, prior to starting the experiment.

Default Value: Automatic

Default Calculation: Automatically resolves to True if any Mix related options are set. Otherwise, resolves to False.

Pattern Description: True or False or Null.

Programmatic Pattern: (BooleanP | Automatic) | Null

Index Matches to: experiment samples

MixType

Indicates the style of motion used to mix the sample, prior to starting the experiment.

Default Value: Automatic

Default Calculation: Automatically resolves based on the container of the sample and the Mix option.

Pattern Description: Roll, Vortex, Sonicate, Pipette, Invert, Stir, Shake, Homogenize, Swirl, Disrupt, or Nutate or Null.

Programmatic Pattern: (MixTypeP | Automatic) | Null

Index Matches to: experiment samples

MixUntilDissolved

Indicates if the mix should be continued up to the MaxIncubationTime or MaxNumberOfMixes (chosen according to the mix Type), in an attempt dissolve any solute. Any mixing/incubation will occur prior to starting the experiment.

Default Value: Automatic

Default Calculation: Automatically resolves to True if MaxIncubationTime or MaxNumberOfMixes is set.

Pattern Description: True or False or Null.

Programmatic Pattern: (BooleanP | Automatic) | Null

Index Matches to: experiment samples

MaxIncubationTime

Maximum duration of time for which the samples will be mixed while incubated in an attempt to dissolve any solute, if the MixUntilDissolved option is chosen. This occurs prior to starting the experiment.

Default Value: Automatic

Default Calculation: Automatically resolves based on MixType, MixUntilDissolved, and the container of the given sample.

Pattern Description: Greater than or equal to 1 minute and less than or equal to 72 hours or Null.

Programmatic Pattern: (RangeP[1*Minute, $MaxExperimentTime] | Automatic) | Null

Index Matches to: experiment samples

IncubationInstrument

The instrument used to perform the Mix and/or Incubation, prior to starting the experiment.

Default Value: Automatic

Default Calculation: Automatically resolves based on the options Mix, Temperature, MixType and container of the sample.

Pattern Description: An object of type or subtype Model[Instrument, Roller], Model[Instrument, OverheadStirrer], Model[Instrument, Vortex], Model[Instrument, Shaker], Model[Instrument, BottleRoller], Model[Instrument, Roller], Model[Instrument, Sonicator], Model[Instrument, HeatBlock], Model[Instrument, Homogenizer], Model[Instrument, Disruptor], Model[Instrument, Nutator], Model[Instrument, Thermocycler], Model[Instrument, EnvironmentalChamber], Model[Instrument, Pipette], Object[Instrument, Roller], Object[Instrument, OverheadStirrer], Object[Instrument, Vortex], Object[Instrument, Shaker], Object[Instrument, BottleRoller], Object[Instrument, Roller], Object[Instrument, Sonicator], Object[Instrument, HeatBlock], Object[Instrument, Homogenizer], Object[Instrument, Disruptor], Object[Instrument, Nutator], Object[Instrument, Thermocycler], Object[Instrument, EnvironmentalChamber], or Object[Instrument, Pipette] or Null.

Programmatic Pattern: (ObjectP[Join[MixInstrumentModels, MixInstrumentObjects]] | Automatic) | Null

Index Matches to: experiment samples

AnnealingTime

Minimum duration for which the SamplesIn should remain in the incubator allowing the system to settle to room temperature after the IncubationTime has passed but prior to starting the experiment.

Default Value: Automatic

Pattern Description: Greater than or equal to 0 minutes and less than or equal to 72 hours or Null.

Programmatic Pattern: (RangeP[0*Minute, $MaxExperimentTime] | Automatic) | Null

Index Matches to: experiment samples

IncubateAliquotContainer

The desired type of container that should be used to prepare and house the incubation samples which should be used in lieu of the SamplesIn for the experiment.

Default Value: Automatic

Pattern Description: An object of type or subtype Model[Container] or {Index, Container} or Null.

Programmatic Pattern: ((ObjectP[Model[Container]] | {GreaterEqualP[1, 1] | (Automatic | Null), (ObjectP[{Model[Container], Object[Container]}] | _String) | Automatic}) | Automatic) | Null

Index Matches to: experiment samples

IncubateAliquotDestinationWell

The desired position in the corresponding IncubateAliquotContainer in which the aliquot samples will be placed.

Default Value: Automatic

Default Calculation: Automatically resolves to A1 in containers with only one position. For plates, fills wells in the order provided by the function AllWells.

Pattern Description: Any well from A1 to H12 or Null.

Programmatic Pattern: (WellPositionP | Automatic) | Null

Index Matches to: experiment samples

IncubateAliquot

The amount of each sample that should be transferred from the SamplesIn into the IncubateAliquotContainer when performing an aliquot before incubation.

Default Value: Automatic

Default Calculation: Automatically set as the smaller between the current sample volume and the maximum volume of the destination container.

Pattern Description: All or greater than or equal to 1 microliter and less than or equal to 20 liters or Null.

Programmatic Pattern: ((RangeP[1*Microliter, 20*Liter] | All) | Automatic) | Null

Index Matches to: experiment samples

Preparatory Centrifugation

Centrifuge

Indicates if the SamplesIn should be centrifuged prior to starting the experiment or any aliquoting. Sample Preparation occurs in the order of Incubation, Centrifugation, Filtration, and then Aliquoting (if specified).

Default Value: Automatic

Default Calculation: Resolves to True if any of the corresponding Centrifuge options are set. Otherwise, resolves to False.

Pattern Description: True or False.

Programmatic Pattern: BooleanP | Automatic

Index Matches to: experiment samples

CentrifugeInstrument

The centrifuge that will be used to spin the provided samples prior to starting the experiment.

Default Value: Automatic

Pattern Description: An object of type or subtype Model[Instrument, Centrifuge] or Object[Instrument, Centrifuge] or Null.

Programmatic Pattern: (ObjectP[{Model[Instrument, Centrifuge], Object[Instrument, Centrifuge]}] | Automatic) | Null

Index Matches to: experiment samples

CentrifugeIntensity

The rotational speed or the force that will be applied to the samples by centrifugation prior to starting the experiment.

Default Value: Automatic

Pattern Description: Greater than 0 revolutions per minute or greater than 0 standard accelerations due to gravity on the surface of the earth or Null.

Programmatic Pattern: ((GreaterP[0*RPM] | GreaterP[0*GravitationalAcceleration]) | Automatic) | Null

Index Matches to: experiment samples

CentrifugeTime

The amount of time for which the SamplesIn should be centrifuged prior to starting the experiment.

Default Value: Automatic

Pattern Description: Greater than 0 minutes or Null.

Programmatic Pattern: (GreaterP[0*Minute] | Automatic) | Null

Index Matches to: experiment samples

CentrifugeTemperature

The temperature at which the centrifuge chamber should be held while the samples are being centrifuged prior to starting the experiment.

Default Value: Automatic

Pattern Description: Ambient or greater than or equal to -10 degrees Celsius and less than or equal to 40 degrees Celsius or Null.

Programmatic Pattern: ((Ambient | RangeP[-10*Celsius, 40*Celsius]) | Automatic) | Null

Index Matches to: experiment samples

CentrifugeAliquotContainer

The desired type of container that should be used to prepare and house the centrifuge samples which should be used in lieu of the SamplesIn for the experiment.

Default Value: Automatic

Pattern Description: An object of type or subtype Model[Container] or {Index, Container} or Null.

Programmatic Pattern: ((ObjectP[Model[Container]] | {GreaterEqualP[1, 1] | (Automatic | Null), (ObjectP[{Model[Container], Object[Container]}] | _String) | Automatic}) | Automatic) | Null

Index Matches to: experiment samples

CentrifugeAliquotDestinationWell

The desired position in the corresponding AliquotContainer in which the aliquot samples will be placed.

Default Value: Automatic

Default Calculation: Automatically resolves to A1 in containers with only one position. For plates, fills wells in the order provided by the function AllWells.

Pattern Description: Any well from A1 to H12 or Null.

Programmatic Pattern: (WellPositionP | Automatic) | Null

Index Matches to: experiment samples

CentrifugeAliquot

The amount of each sample that should be transferred from the SamplesIn into the CentrifugeAliquotContainer when performing an aliquot before centrifugation.

Default Value: Automatic

Default Calculation: Automatically set as the smaller between the current sample volume and the maximum volume of the destination container.

Pattern Description: All or greater than or equal to 1 microliter and less than or equal to 20 liters or Null.

Programmatic Pattern: ((RangeP[1*Microliter, 20*Liter] | All) | Automatic) | Null

Index Matches to: experiment samples

Preparatory Filtering

Filtration

Indicates if the SamplesIn should be filter prior to starting the experiment or any aliquoting. Sample Preparation occurs in the order of Incubation, Centrifugation, Filtration, and then Aliquoting (if specified).

Default Value: Automatic

Default Calculation: Resolves to True if any of the corresponding Filter options are set. Otherwise, resolves to False.

Pattern Description: True or False.

Programmatic Pattern: BooleanP | Automatic

Index Matches to: experiment samples

FiltrationType

The type of filtration method that should be used to perform the filtration.

Default Value: Automatic

Default Calculation: Will automatically resolve to a filtration type appropriate for the volume of sample being filtered.

Pattern Description: PeristalticPump, Centrifuge, Vacuum, Syringe, or AirPressure or Null.

Programmatic Pattern: (FiltrationTypeP | Automatic) | Null

Index Matches to: experiment samples

FilterInstrument

The instrument that should be used to perform the filtration.

Default Value: Automatic

Default Calculation: Will automatically resolved to an instrument appropriate for the filtration type.

Pattern Description: An object of type or subtype Model[Instrument, FilterBlock], Object[Instrument, FilterBlock], Model[Instrument, PeristalticPump], Object[Instrument, PeristalticPump], Model[Instrument, VacuumPump], Object[Instrument, VacuumPump], Model[Instrument, Centrifuge], Object[Instrument, Centrifuge], Model[Instrument, SyringePump], or Object[Instrument, SyringePump] or Null.

Programmatic Pattern: (ObjectP[{Model[Instrument, FilterBlock], Object[Instrument, FilterBlock], Model[Instrument, PeristalticPump], Object[Instrument, PeristalticPump], Model[Instrument, VacuumPump], Object[Instrument, VacuumPump], Model[Instrument, Centrifuge], Object[Instrument, Centrifuge], Model[Instrument, SyringePump], Object[Instrument, SyringePump]}] | Automatic) | Null

Index Matches to: experiment samples

Filter

The filter that should be used to remove impurities from the SamplesIn prior to starting the experiment.

Default Value: Automatic

Default Calculation: Will automatically resolve to a filter appropriate for the filtration type and instrument.

Pattern Description: An object of type or subtype Model[Container, Plate, Filter], Model[Container, Vessel, Filter], or Model[Item, Filter] or Null.

Programmatic Pattern: (ObjectP[{Model[Container, Plate, Filter], Model[Container, Vessel, Filter], Model[Item, Filter]}] | Automatic) | Null

Index Matches to: experiment samples

FilterMaterial

The membrane material of the filter that should be used to remove impurities from the SamplesIn prior to starting the experiment.

Default Value: Automatic

Default Calculation: Resolves to an appropriate filter material for the given sample is Filtration is set to True.

Pattern Description: Cellulose, Cotton, Polyethylene, PTFE, Nylon, PES, PLUS, PVDF, GlassFiber, GHP, UHMWPE, EPDM, DuraporePVDF, GxF, ZebaDesaltingResin, NickelResin, Silica, or HLB or Null.

Programmatic Pattern: (FilterMembraneMaterialP | Automatic) | Null

Index Matches to: experiment samples

PrefilterMaterial

The material from which the prefilter filtration membrane should be made of to remove impurities from the SamplesIn prior to starting the experiment.

Default Value: Automatic

Default Calculation: By default, no prefiltration is performed on samples, even when Filter->True.

Pattern Description: Cellulose, Cotton, Polyethylene, PTFE, Nylon, PES, PLUS, PVDF, GlassFiber, GHP, UHMWPE, EPDM, DuraporePVDF, GxF, ZebaDesaltingResin, NickelResin, Silica, or HLB or Null.

Programmatic Pattern: (FilterMembraneMaterialP | Automatic) | Null

Index Matches to: experiment samples

FilterPoreSize

The pore size of the filter that should be used when removing impurities from the SamplesIn prior to starting the experiment.

Default Value: Automatic

Default Calculation: Resolves to an appropriate filter pore size for the given sample is Filtration is set to True.

Pattern Description: 0.008 micrometers, 0.1 micrometers, 0.2 micrometers, 0.22 micrometers, 0.45 micrometers, 1. micrometer, 1.1 micrometers, 2.5 micrometers, 6. micrometers, 20. micrometers, 30. micrometers, or 100. micrometers or Null.

Programmatic Pattern: (FilterSizeP | Automatic) | Null

Index Matches to: experiment samples

PrefilterPoreSize

The pore size of the filter; all particles larger than this should be removed during the filtration.

Default Value: Automatic

Default Calculation: By default, no prefiltration is performed on samples, even when Filter->True.

Pattern Description: 0.008 micrometers, 0.1 micrometers, 0.2 micrometers, 0.22 micrometers, 0.45 micrometers, 1. micrometer, 1.1 micrometers, 2.5 micrometers, 6. micrometers, 20. micrometers, 30. micrometers, or 100. micrometers or Null.

Programmatic Pattern: (FilterSizeP | Automatic) | Null

Index Matches to: experiment samples

FilterSyringe

The syringe used to force that sample through a filter.

Default Value: Automatic

Default Calculation: Resolves to an syringe appropriate to the volume of sample being filtered, if Filtration is set to True.

Pattern Description: An object of type or subtype Model[Container, Syringe] or Object[Container, Syringe] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Model[Container, Syringe], Object[Container, Syringe]}] | _String) | Automatic) | Null

Index Matches to: experiment samples

FilterHousing

The filter housing that should be used to hold the filter membrane when filtration is performed using a standalone filter membrane.

Default Value: Automatic

Default Calculation: Resolve to an housing capable of holding the size of the membrane being used, if filter with Membrane FilterType is being used and Filtration is set to True.

Pattern Description: An object of type or subtype Model[Instrument, FilterHousing], Object[Instrument, FilterHousing], Model[Instrument, FilterBlock], or Object[Instrument, FilterBlock] or Null.

Programmatic Pattern: (ObjectP[{Model[Instrument, FilterHousing], Object[Instrument, FilterHousing], Model[Instrument, FilterBlock], Object[Instrument, FilterBlock]}] | Automatic) | Null

Index Matches to: experiment samples

FilterIntensity

The rotational speed or force at which the samples will be centrifuged during filtration.

Default Value: Automatic

Default Calculation: Will automatically resolve to 2000 GravitationalAcceleration if FiltrationType is Centrifuge and Filtration is True.

Pattern Description: Greater than 0 revolutions per minute or greater than 0 standard accelerations due to gravity on the surface of the earth or Null.

Programmatic Pattern: ((GreaterP[0*RPM] | GreaterP[0*GravitationalAcceleration]) | Automatic) | Null

Index Matches to: experiment samples

FilterTime

The amount of time for which the samples will be centrifuged during filtration.

Default Value: Automatic

Default Calculation: Will automatically resolve to 5 Minute if FiltrationType is Centrifuge and Filtration is True.

Pattern Description: Greater than 0 minutes or Null.

Programmatic Pattern: (GreaterP[0*Minute] | Automatic) | Null

Index Matches to: experiment samples

FilterTemperature

The temperature at which the centrifuge chamber will be held while the samples are being centrifuged during filtration.

Default Value: Automatic

Default Calculation: Will automatically resolve to 22 Celsius if FiltrationType is Centrifuge and Filtration is True.

Pattern Description: Greater than or equal to 4 degrees Celsius or Null.

Programmatic Pattern: ((Alternatives[GreaterEqualP[4*Celsius]]) | Automatic) | Null

Index Matches to: experiment samples

FilterContainerOut

The desired container filtered samples should be produced in or transferred into by the end of filtration, with indices indicating grouping of samples in the same plates, if desired.

Default Value: Automatic

Default Calculation: Automatically set as the PreferredContainer for the Volume of the sample. For plates, attempts to fill all wells of a single plate with the same model before using another one.

Pattern Description: An object of type or subtype Model[Container] or Object[Container] or a prepared sample or {Index, Container} or Null.

Programmatic Pattern: (((ObjectP[{Model[Container], Object[Container]}] | _String) | {GreaterEqualP[1, 1] | Automatic, (ObjectP[{Model[Container], Object[Container]}] | _String) | Automatic}) | Automatic) | Null

Index Matches to: experiment samples

FilterAliquotDestinationWell

The desired position in the corresponding AliquotContainer in which the aliquot samples will be placed.

Default Value: Automatic

Default Calculation: Automatically resolves to A1 in containers with only one position. For plates, fills wells in the order provided by the function AllWells.

Pattern Description: Any well from A1 to H12 or Null.

Programmatic Pattern: (WellPositionP | Automatic) | Null

Index Matches to: experiment samples

FilterAliquotContainer

The desired type of container that should be used to prepare and house the filter samples which should be used in lieu of the SamplesIn for the experiment.

Default Value: Automatic

Pattern Description: An object of type or subtype Model[Container] or {Index, Container} or Null.

Programmatic Pattern: ((ObjectP[Model[Container]] | {GreaterEqualP[1, 1] | (Automatic | Null), (ObjectP[{Model[Container], Object[Container]}] | _String) | Automatic}) | Automatic) | Null

Index Matches to: experiment samples

FilterAliquot

The amount of each sample that should be transferred from the SamplesIn into the FilterAliquotContainer when performing an aliquot before filtration.

Default Value: Automatic

Default Calculation: Automatically set as the smaller between the current sample volume and the maximum volume of the destination container.

Pattern Description: All or greater than or equal to 1 microliter and less than or equal to 20 liters or Null.

Programmatic Pattern: ((RangeP[1*Microliter, 20*Liter] | All) | Automatic) | Null

Index Matches to: experiment samples

FilterSterile

Indicates if the filtration of the samples should be done in a sterile environment.

Default Value: Automatic

Default Calculation: Resolve to False if Filtration is indicated. If sterile filtration is desired, this option must manually be set to True.

Pattern Description: True or False or Null.

Programmatic Pattern: (BooleanP | Automatic) | Null

Index Matches to: experiment samples

Aliquoting

Aliquot

Indicates if aliquots should be taken from the SamplesIn and transferred into new AliquotSamples used in lieu of the SamplesIn for the experiment. Note that if NumberOfReplicates is specified this indicates that the input samples will also be aliquoted that number of times. Note that Aliquoting (if specified) occurs after any Sample Preparation (if specified).

Default Value: Automatic

Pattern Description: True or False.

Programmatic Pattern: BooleanP | Automatic

Index Matches to: experiment samples

AliquotAmount

The amount of a sample that should be transferred from the input samples into aliquots.

Default Value: Automatic

Default Calculation: Automatically set as the smaller between the current sample volume and the maximum volume of the destination container if a liquid, or the current Mass or Count if a solid or counted item, respectively.

Pattern Description: All or Count or Count or Mass or Volume or Null.

Programmatic Pattern: ((RangeP[1*Microliter, 20*Liter] | RangeP[1*Milligram, 20*Kilogram] | GreaterP[0*Unit, 1*Unit] | GreaterP[0., 1.] | All) | Automatic) | Null

Index Matches to: experiment samples

TargetConcentration

The desired final concentration of analyte in the AliquotSamples after dilution of aliquots of SamplesIn with the ConcentratedBuffer and BufferDiluent which should be used in lieu of the SamplesIn for the experiment.

Default Value: Automatic

Default Calculation: Automatically calculated based on aliquot and buffer volumes.

Pattern Description: Greater than 0 molar or greater than 0 grams per liter or Null.

Programmatic Pattern: ((GreaterP[0*Molar] | GreaterP[0*(Gram/Liter)]) | Automatic) | Null

Index Matches to: experiment samples

TargetConcentrationAnalyte

The substance whose final concentration is attained with the TargetConcentration option.

Default Value: Automatic

Default Calculation: Automatically set to the first value in the Analytes field of the input sample, or, if not populated, to the first analyte in the Composition field of the input sample, or if none exist, the first identity model of any kind in the Composition field.

Pattern Description: An object of type or subtype Model[Molecule], Model[Molecule, cDNA], Model[Molecule, Oligomer], Model[Molecule, Transcript], Model[Molecule, Protein], Model[Molecule, Protein, Antibody], Model[Molecule, Carbohydrate], Model[Molecule, Polymer], Model[Resin], Model[Resin, SolidPhaseSupport], Model[Lysate], Model[ProprietaryFormulation], Model[Virus], Model[Cell], Model[Cell, Mammalian], Model[Cell, Bacteria], Model[Cell, Yeast], Model[Tissue], Model[Material], or Model[Species] or Null.

Programmatic Pattern: (ObjectP[IdentityModelTypes] | Automatic) | Null

Index Matches to: experiment samples

AssayVolume

The desired total volume of the aliquoted sample plus dilution buffer.

Default Value: Automatic

Default Calculation: Automatically determined based on Volume and TargetConcentration option values.

Pattern Description: Greater than or equal to 1 microliter and less than or equal to 20 liters or Null.

Programmatic Pattern: (RangeP[1*Microliter, 20*Liter] | Automatic) | Null

Index Matches to: experiment samples

ConcentratedBuffer

The concentrated buffer which should be diluted by the BufferDilutionFactor in the final solution (i.e., the combination of the sample, ConcentratedBuffer, and BufferDiluent). The ConcentratedBuffer and BufferDiluent will be combined and then mixed with the sample, where the combined volume of these buffers is the difference between the AliquotAmount and the total AssayVolume.

Default Value: Automatic

Pattern Description: An object of type or subtype Model[Sample] or Object[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Model[Sample], Object[Sample]}] | _String) | Automatic) | Null

Index Matches to: experiment samples

BufferDilutionFactor

The dilution factor by which the concentrated buffer should be diluted in the final solution (i.e., the combination of the sample, ConcentratedBuffer, and BufferDiluent). The ConcentratedBuffer and BufferDiluent will be combined and then mixed with the sample, where the combined volume of these buffers is the difference between the AliquotAmount and the total AssayVolume.

Default Value: Automatic

Default Calculation: If ConcentratedBuffer is specified, automatically set to the ConcentratedBufferDilutionFactor of that sample; otherwise, set to Null.

Pattern Description: Greater than or equal to 1 or Null.

Programmatic Pattern: (GreaterEqualP[1] | Automatic) | Null

Index Matches to: experiment samples

BufferDiluent

The buffer used to dilute the aliquot sample such that ConcentratedBuffer is diluted by BufferDilutionFactor in the final solution. The ConcentratedBuffer and BufferDiluent will be combined and then mixed with the sample, where the combined volume of these buffers is the difference between the AliquotAmount and the total AssayVolume.

Default Value: Automatic

Default Calculation: Automatically resolves to Model[Sample, "Milli-Q water"] if ConcentratedBuffer is specified; otherwise, resolves to Null.

Pattern Description: An object of type or subtype Model[Sample] or Object[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Model[Sample], Object[Sample]}] | _String) | Automatic) | Null

Index Matches to: experiment samples

AssayBuffer

The buffer that should be added to any aliquots requiring dilution, where the volume of this buffer added is the difference between the AliquotAmount and the total AssayVolume.

Default Value: Automatic

Default Calculation: Automatically resolves to Model[Sample, "Milli-Q water"] if ConcentratedBuffer is not specified; otherwise, resolves to Null.

Pattern Description: An object of type or subtype Model[Sample] or Object[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Model[Sample], Object[Sample]}] | _String) | Automatic) | Null

Index Matches to: experiment samples

AliquotSampleStorageCondition

The non-default conditions under which any aliquot samples generated by this experiment should be stored after the protocol is completed.

Default Value: Automatic

Pattern Description: {AmbientStorage, Refrigerator, Freezer, DeepFreezer, CryogenicStorage, YeastIncubation, BacteriaIncubation, MammalianIncubation, TissueCultureCellsIncubation, MicrobialCellsIncubation, MicrobialCellsShakingIncubation, YeastCellsIncubation, YeastCellsShakingIncubation, ViralIncubation, AcceleratedTesting, IntermediateTesting, LongTermTesting, UVVisLightTesting} or Disposal or Null.

Programmatic Pattern: ((SampleStorageTypeP | Disposal) | Automatic) | Null

Index Matches to: experiment samples

DestinationWell

The desired position in the corresponding AliquotContainer in which the aliquot samples will be placed.

Default Value: Automatic

Default Calculation: Automatically resolves to A1 in containers with only one position. For plates, fills wells in the order provided by the function AllWells.

Pattern Description: Any well from A1 to H12 or list of one or more any well from A1 to H12 or any well from A1 to H12 entries or Null.

Programmatic Pattern: ((WellPositionP | {((Automatic | Null) | WellPositionP)..}) | Automatic) | Null

AliquotContainer

The desired type of container that should be used to prepare and house the aliquot samples, with indices indicating grouping of samples in the same plates, if desired. This option will resolve to be the length of the SamplesIn * NumberOfReplicates.

Default Value: Automatic

Default Calculation: Automatically set as the PreferredContainer for the AssayVolume of the sample. For plates, attempts to fill all wells of a single plate with the same model before aliquoting into the next.

Pattern Description: An object of type or subtype Model[Container] or Object[Container] or a prepared sample or Automatic or Null or {Index, Container} or list of one or more an object of type or subtype Model[Container] or Object[Container] or a prepared sample or Automatic or Null entries or list of one or more Automatic or Null or {Index, Container} entries.

Programmatic Pattern: (((ObjectP[{Model[Container], Object[Container]}] | _String) | (Automatic | Null) | {GreaterEqualP[1, 1] | (Automatic | Null), (ObjectP[{Model[Container], Object[Container]}] | _String) | (Automatic | Null)} | {((ObjectP[{Model[Container], Object[Container]}] | _String) | (Automatic | Null))..} | {({GreaterEqualP[1, 1] | (Automatic | Null), (ObjectP[{Model[Container], Object[Container]}] | _String) | (Automatic | Null)} | (Automatic | Null))..}) | Automatic) | Null

AliquotPreparation

Indicates the desired scale at which liquid handling used to generate aliquots will occur.

Default Value: Automatic

Default Calculation: Automatic resolution will occur based on manipulation volumes and container types.

Pattern Description: Manual or Robotic or Null.

Programmatic Pattern: (PreparationMethodP | Automatic) | Null

ConsolidateAliquots

Indicates if identical aliquots should be prepared in the same container/position.

Default Value: Automatic

Pattern Description: True or False or Null.

Programmatic Pattern: (BooleanP | Automatic) | Null



Organizational Information

Template

A template protocol whose methodology should be reproduced in running this experiment. Option values will be inherited from the template protocol, but can be individually overridden by directly specifying values for those options to this Experiment function.

Default Value: Null

Pattern Description: An object of type or subtype Object[Protocol] or an object of type or subtype of Object[Protocol] with UnresolvedOptions, ResolvedOptions specified or Null.

Programmatic Pattern: (ObjectP[Object[Protocol]] | FieldReferenceP[Object[Protocol], {UnresolvedOptions, ResolvedOptions}]) | Null

Name

A object name which should be used to refer to the output object in lieu of an automatically generated ID number.

Default Value: Null

Pattern Description: A string or Null.

Programmatic Pattern: _String | Null

Post Experiment

MeasureWeight

Indicates if any solid samples that are modified in the course of the experiment should have their weights measured and updated after running the experiment. Please note that public samples are weighed regardless of the value of this option.

Default Value: Automatic

Pattern Description: True or False or Null.

Programmatic Pattern: (BooleanP | Automatic) | Null

MeasureVolume

Indicates if any liquid samples that are modified in the course of the experiment should have their volumes measured and updated after running the experiment. Please note that public samples are volume measured regardless of the value of this option.

Default Value: Automatic

Pattern Description: True or False or Null.

Programmatic Pattern: (BooleanP | Automatic) | Null

ImageSample

Indicates if any samples that are modified in the course of the experiment should be freshly imaged after running the experiment. Please note that public samples are imaged regardless of the value of this option.

Default Value: Automatic

Pattern Description: True or False or Null.

Programmatic Pattern: (BooleanP | Automatic) | Null



Kinetics

Measure the association and dissociation behavior of a dilution series for a single sample:

ExperimentBioLayerInterferometry[mySample, ExperimentType -> Kinetics]

Measure the association and dissociation behavior of dilutions series of set of samples:

ExperimentBioLayerInterferometry[{mySample1, mySample2, mySample3},

 ExperimentType -> Kinetics]

Quantitation

Quantify the amount of an analyte in a given sample using direct measurement and a calibration curve:

ExperimentBioLayerInterferometry[mySample,

 	ExperimentType -> Quantitation,

 	QuantitationParameters -> {StandardCurve},

 	QuantitationStandard ->

  Object[Sample, "standard solution for calibration curve"]

 ]

Quantify the amount of an analyte in a given sample using indirect (amplified) detection. This is useful in cases where analyte association does not appreciably change the biolayer thickness:

ExperimentBioLayerInterferometry[mySample,

 	ExperimentType -> Quantitation,

 	QuantitationParameters -> {StandardCurve, AmplifiedDetection},

 	QuantitationStandard ->

  Object[Sample, "standard solution for calibration curve"],

 	AmplifiedDetectionSolution -> Object[Sample, "Amplifying solution"]

 ]

Quantify the amount of an analyte in a given sample by specifying a standard curve with fixed dilutions in the form of {Standard Volume, Diluent Volume, Temporary Solution Name}:

ExperimentBioLayerInterferometry[mySample,

 	ExperimentType -> Quantitation,

 	QuantitationParameters -> {StandardCurve},

 	QuantitationStandard ->

  Object[Sample, "standard solution for calibration curve"],

 	QuantitationStandardFixedDilutions -> {

   		{100 * Microliter, 100 * Microliter, "2x dilution"},

   		{50 * Microliter, 150 * Microliter, "4x dilution"},

   		{20 * Microliter, 180 * Microliter, "10x dilution"},

   		{10 * Microliter, 190 * Microliter, "20 x dilution"}

   	}

 ]

Quantify the amount of an analyte in a given sample by specifying a standard curve with serial dilutions in the form of {Dilution Factor, Number Of Dilutions, {Temporary Solution Names}}:

ExperimentBioLayerInterferometry[mySample,

 	ExperimentType -> Quantitation,

 	QuantitationParameters -> {StandardCurve},

 	QuantitationStandard ->

  Object[Sample, "standard solution for calibration curve"],

 	QuantitationStandardSerialDilutions -> {5,

   4, {"5x dilution", "25x dilution", "125x dilution",

    "625x dilution"}}

 ]

Epitope Binning

Group antibodies by the epitope they bind in a given antigen:

ExperimentBioLayerInterferometry[

 	{mySample1, mySample2, mySample3, mySample4, mySample5, mySample6,

  mySample7},

 	ExperimentType -> EpitopeBinning,

 	BinningAntigen -> Object[Sample, "binning antigen solution"]

 ]

Screening

Test specific pairs of immobilized and solution species to qualitatively assess their binding affinity:

ExperimentBioLayerInterferometry[{mySample1, mySample2},

 	ExperimentType -> AssayDevelopment,

 	DevelopmentType -> ScreenInteraction,

 	TestInteractionSolutions -> {

   		Object[Sample, "loading solution 1"],

   		Object[Sample, "loading solution 2"]

   	}

 ]

Test the efficacy of a given regeneration solution:

ExperimentBioLayerInterferometry[mySample,

 	ExperimentType -> AssayDevelopment,

 	DevelopmentType -> ScreenRegeneration,

 	RegenerationType -> {Regenerate},

 	TestRegenerationSolutions -> {

   		Object[Sample, "regen solution 1"],

   		Object[Sample, "regen solution 2"]

   	}

 ]



Preferred Input Containers

The experiment takes common liquid handler compatible containers.



Possible Issues

Sample evaporation

Assays longer than 4 hours may exhibit excessive evaporation which can impact experimental results. In this case, it is recommended that a plate cover be used to limit evaporation.

Insufficient well volume

Well volumes below 200 uL may result in sensor failure or inaccurate data due to incomplete probe immersion. Evaporation can be prevented by using the AssayPlateCover option.

Insufficient probe hydration

Probes should be immersed in buffer solution for at least 10 minutes prior to the assay beginning. Insufficient probe equilibration can lead to sensor failure. The use of the ProbeRackEquilibration option is highly recommended and will generally prevent this issue.

Baseline drift

The data may drift over time. This may be a result of incomplete probe equilibration.

Nonspecific binding

Nonspecific binding may occur in cases where the surface is not properly passivated or a suboptimal buffer is selected. The suggested remedy is to screen buffers or quench solutions to find a suitable solution.

Overloaded probe surface

Over-saturation of the probe surface may lead to overcrowding of the probe surface and misleading kinetic data. If probe surface saturation appears problematic, as indicated by abnormal association and dissociation curves, try loading for a shorter period of time or in a more dilute solution.

[end context 1]

Here are summaries of the previous meetings:

[begin summary 1]

### Comprehensive Protocol for Peptide Synthesis and Validation

This protocol integrates the best components from previous summaries to ensure a detailed, efficient, and scientifically rigorous approach to peptide synthesis and validation, aligned with the project's goals and constraints.

---

### Peptide Synthesis Protocol

#### Step 1: Solid-Phase Peptide Synthesis (SPPS)
- **Experiment**: `ExperimentPeptideSynthesis`
- **Inputs**: 
  - Fmoc-protected amino acids: 0.1 M in NMP, stored at 4°C
  - Rink amide resin: 1 g, 0.1 mmol/g loading capacity
  - Coupling reagents: HBTU (0.1 M in DMF), DIPEA (2 M in NMP)
  - Deprotection agent: 20% piperidine in DMF, freshly prepared
- **Equipment**: 
  - Automated peptide synthesizer, calibrated for accurate volume delivery
- **Conditions**: 
  - Resin swelling in DMF for 30 minutes
  - Coupling: 5 mL amino acid solution, 5 mL HBTU, 2 mL DIPEA, stir for 60 minutes
  - Deprotection: 10 mL of 20% piperidine in DMF for 20 minutes, repeated
  - Washing: Three washes with 10 mL DMF after each step
- **Output**: Peptide-resin with confirmed coupling efficiency via HPLC

**Quality Control**:
- **Coupling Check**: Perform Kaiser test after each coupling step
- **Documentation**: Record reagent batch numbers, conditions, and deviations

#### Step 2: Cleavage and Deprotection
- **Experiment**: `ExperimentCleavage`
- **Inputs**:
  - Cleavage cocktail: TFA:water:triisopropylsilane:ethyl methyl sulfide (95:2.5:1:1.5), 10 mL per gram of resin
- **Conditions**: 
  - Cleavage at room temperature for 2-3 hours
- **Output**: Crude peptide in solution

#### Step 3: Purification
- **Experiment**: `ExperimentSolidPhaseExtraction` and `ExperimentHPLC`
- **Inputs**: 
  - Crude peptide solution
  - Solvent system: 0.1% TFA in acetonitrile-water gradient
- **Equipment**: 
  - SPE apparatus and HPLC system with C18 column
- **Conditions**: 
  - SPE: Gradient from 5% to 95% acetonitrile over 30 minutes
  - HPLC: Flow rate 1 mL/min, UV detection at 214 nm
- **Output**: Purified peptide >90% purity

#### Step 4: Mass Confirmation
- **Experiment**: `ExperimentLCMS`
- **Inputs**: 
  - Purified peptide
- **Equipment**: 
  - LC-MS system
- **Conditions**: 
  - Standard LCMS settings for peptide analysis
- **Output**: Confirmed molecular weight and sequence identity

#### Step 5: Chemical Modifications
- **Experiment**: `ExperimentBioconjugation`
- **Inputs**: 
  - Purified peptide (0.4 mmol)
  - PEG reagent (0.48 mmol)
- **Conditions**: 
  - Room temperature, stirring for 2 hours in PBS
- **Output**: Modified peptide, confirmed by MS

### Peptide Validation Protocol

#### Structural Validation
- **Experiment**: `ExperimentNMR` and `ExperimentCircularDichroism`
- **Inputs**: 
  - PEGylated peptide
  - PBS buffer (pH 7.4)
- **Equipment**: 
  - NMR spectrometer and CD spectrometer
- **Conditions**: 
  - NMR: Proton and COSY 2D in DMSO-d6
  - CD: 190-260 nm at 25°C
- **Output**: Structural integrity and secondary structure confirmation

#### Binding Validation
- **Experiment**: `ExperimentBioLayerInterferometry` and `ExperimentFluorescencePolarization`
- **Inputs**: 
  - PEGylated peptide
  - Target protein: 1 mg/mL in PBS
- **Equipment**: 
  - BLI instrument and fluorescence polarization reader
- **Conditions**: 
  - BLI: Measure kinetics at peptide concentrations from 1 nM to 1 µM
  - FP: Label peptide with FITC, measure binding across concentrations
- **Output**: Binding affinity (expected KD <10 nM) and kinetic data

#### Functional Validation
- **Experiment**: `ExperimentELISA`
- **Inputs**: 
  - PEGylated peptide
  - HRP-conjugated secondary antibodies
- **Equipment**: 
  - ELISA plate reader
- **Conditions**: 
  - Standard ELISA protocol
- **Output**: Quantitative binding data

#### Stability Validation
- **Experiment**: `ExperimentThermalShift`
- **Inputs**: 
  - PEGylated peptide
  - Sypro Orange dye
- **Equipment**: 
  - Real-time PCR thermal cycler
- **Conditions**: 
  - Heat and record fluorescence to determine melting temperature
- **Output**: Thermal stability profile

### Integration with Machine Learning Models

- **Data Handling and Feedback**: Collect binding affinity, structural data, and stability profiles to feed back into machine learning models (ProteinMPNN and RFDiffusion). Use these data to refine predictions, focusing on recognized patterns or discrepancies.

### Controls and Quality Assurance

- **Control Samples**: Include non-modified peptides as negative controls and known active peptides as positive controls.
- **Quality Assurance**: Implement checkpoints for purity (>90%) and identity verification using LCMS and HPLC. Document each step thoroughly.
- **Sample Management**: Use barcoded sample tracking within ECL to ensure precise handling and accountability.

### Data Management and Feedback Loop

- **Data Management Tools**: Use platforms like AWS for data storage and management. Continuously integrate experimental data back into the machine learning models to refine predictions.
- **Feedback Loop**: Regularly update models with new data, possibly weekly or bi-weekly, to enhance prediction accuracy and guide iterative peptide design.

---

### Explanation of Component Selection

1. **Detailed Reagent Preparation and Equipment Use**: This was emphasized in summaries 2 and 5, ensuring precise conditions and reagent handling, which is critical for reproducibility and accuracy.

2. **Integration with Machine Learning**: Summaries 3 and 4 highlighted the use of machine learning models like ProteinMPNN and RFDiffusion, which is crucial for aligning with the project's goal of scientifically impactful applications.

3. **Quality Assurance and Controls**: Summaries 1 and 5 provided comprehensive quality control measures, ensuring that each step is validated and documented, which is essential for high clinical value and scientific rigor.

4. **Data Management and Feedback Loop**: Summaries 4 and 5 focused on using AWS for data management and creating a feedback loop with machine learning models, ensuring continuous improvement and alignment with project goals.

By integrating these components, the protocol is robust, detailed, and aligned with the project's objectives, ensuring high clinical value and impactful scientific contributions.

[end summary 1]

Here is the agenda for the meeting:

You are working on a research project to use machine learning for drug discovery. Your goals are the following: (1) the project must have high clinical value, meaning the research contributes to helping patients, (2) the project must include a scientifically impactful application of machine learning to drug discovery, and (3) the project must use Emerald Cloud Labs (ECL) for all experimental validation with a 3-month limit on experiments. Your team previously decided to pursue peptide-based therapeutics. You previously designed experimental protocols for synthesis and validation of peptides that are designed to bind to a given protein drug target. Now you must implement one of these protocols using ECL. Please implement the ExperimentBioLayerInterferometry protocol using the appropriate commands and syntax from ECL, writing out the experiment in the form ExperimentBioLayerInterferometry[inputs] where you fill in "inputs" with the appropriate inputs. Please refer to the ECL documentation that is provided as context with example function calls and the full set of options for the experiment. In general, leave most options at their default values and therefore do not include them in your experiment function call. Only specify options that must be changed from their default value for your specific experiment. For every option that you specify, please state the default value, the different value you chose, and why you chose that value instead of the default.

Medicinal Chemist, please provide your response to the agenda.

## Medicinal Chemist

To implement the `ExperimentBioLayerInterferometry` protocol using ECL, we need to focus on the key parameters that must be adjusted from their default values to suit our specific experimental needs. Here is a step-by-step breakdown of the experiment setup, including the rationale for each specified option:

### ExperimentBioLayerInterferometry Setup

#### Inputs
- **Samples**: The PEGylated peptide and the target protein solution.
- **ExperimentType**: Kinetics, as we are interested in measuring the binding kinetics between the peptide and the target protein.

#### Specified Options
1. **ExperimentType**
   - **Default Value**: Quantitation
   - **Chosen Value**: Kinetics
   - **Rationale**: We need to measure the association and dissociation rates of the peptide-protein interaction to understand the binding kinetics.

2. **BioProbeType**
   - **Default Value**: Model[Item, BLIProbe, ProA]
   - **Chosen Value**: Model[Item, BLIProbe, ProB]
   - **Rationale**: Depending on the specific chemistry of the peptide and protein, a different probe type may offer better binding characteristics or sensitivity.

3. **NumberOfRepeats**
   - **Default Value**: Null
   - **Chosen Value**: 3
   - **Rationale**: To ensure reproducibility and reliability of the kinetic data, we will repeat the assay three times.

4. **AcquisitionRate**
   - **Default Value**: 5 hertz
   - **Chosen Value**: 10 hertz
   - **Rationale**: A higher acquisition rate is suitable for capturing fast binding events, which is critical for accurately measuring kinetics.

5. **PlateCover**
   - **Default Value**: Automatic
   - **Chosen Value**: True
   - **Rationale**: To prevent evaporation during long assays, especially since kinetic measurements can extend over several hours.

6. **Temperature**
   - **Default Value**: Ambient
   - **Chosen Value**: 25 degrees Celsius
   - **Rationale**: Maintaining a controlled temperature is essential for consistent kinetic measurements.

7. **KineticsSampleFixedDilutions**
   - **Default Value**: Automatic
   - **Chosen Value**: {100 µL, 200 µL, "Sample Dilution"}
   - **Rationale**: To create a series of dilutions for the kinetic analysis, ensuring a range of concentrations are tested.

8. **KineticsSampleDiluent**
   - **Default Value**: Automatic
   - **Chosen Value**: Model[Sample, StockSolution, "PBS"]
   - **Rationale**: PBS is a common buffer for maintaining physiological conditions during binding assays.

### Experiment Function Call
```plaintext
ExperimentBioLayerInterferometry[
    {Object[Sample, "PEGylated peptide"], Object[Sample, "target protein solution"]},
    ExperimentType -> Kinetics,
    BioProbeType -> Model[Item, BLIProbe, ProB],
    NumberOfRepeats -> 3,
    AcquisitionRate -> 10*Hertz,
    PlateCover -> True,
    Temperature -> 25*Celsius,
    KineticsSampleFixedDilutions -> {{100*Microliter, 200*Microliter, "Sample Dilution"}},
    KineticsSampleDiluent -> Model[Sample, StockSolution, "PBS"]
]
```

### Summary
This setup ensures that we are accurately measuring the binding kinetics of our peptide-protein interaction under controlled conditions, with sufficient replicates to ensure data reliability. The use of ECL allows us to efficiently manage and execute this protocol within the 3-month experimental limit, aligning with our project goals of high clinical value and impactful scientific application.
