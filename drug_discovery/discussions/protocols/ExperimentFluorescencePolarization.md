## User

This is the beginning of an individual meeting with Medicinal Chemist to discuss your research project.

Here is context for this meeting:

[begin context 1]

ExperimentFluorescencePolarization[Samples]⟹Protocol

generates a Protocol for measuring fluorescence polarization of the provided Samples.



Fluorescence Polarization (FP) assesses the fraction of tracer bound to receptor by measuring the the molecular rotation of a fluorophore. The principle of FP is that a fluorophore excited by polarized light emits light oriented in a parallel plane. After a fluorescent molecule absorbs excitation light, it tumbles and rotates in solution during the time between excitation and emission. If the molecule is large, it rotates slowly, and the emission light remains largely polarized. Whereas a small, rapidly tumbling molecule rotates quickly and emits depolarized light. Measuring the degree of polarization provides a measure of the fraction of tracer bound to receptor, with applications in receptor-ligand binding, enzymatic degradation, and DNA hybridization studies.



Experimental Principles

Figure 1.1: Procedural overview of a Fluorescence Polarization experiment. Step 1: Samples are prepared in a reader-compatible shallow well plate. Step 2: Injection lines are cleaned and primed. Step 3: The assay plate is optionally held at a specified temperature. Step 4: Injection samples are dispensed into the assay plate. Step 5: The assay plate is shaken. Step 6: The plate reader excites samples with horizontally polarized light and measures emitted light in the horizontal and vertical planes. Large molecules rotate slower than small molecules and reflect more polarized light. Step 7: Optionally follow-up analysis, such as standard curve fitting, can be performed.



Instrumentation

PHERAstar FS

Model[Instrument, PlateReader, "id:01G6nvkKr3o7"]

Figure 2.1.1: The PHERAstar uses optic modules to package excitation and emission filters into a single package. This means wavelength combinations are restricted to those which already exist in the optic module. Up to five excitation/emission pairs can be recorded in a single experiment. Additionally, the PHERAstar supports dual emission so it's possible to record emission data at 2 different wavelengths simultaneously. The plate chamber can be heated up to 45°C and it can mix the plate at up to 700 RPM before and/or during the run. The reader has two 300μL syringe pump injectors which can be used for 0.5 - 300 μL injections of two unique samples at up to four time points during the run. There are two primary kinetics read modes. It can perform all readings, injections and mixing for a single well before moving onto the next well or it can read in cycles, reading all the assay wells in the plate again and again until the RunTime has been reached. The second mode is recommended for most assays, except those that use very fast kinetics.



Experiment Options

Optics

ExcitationWavelength

The wavelength(s) which should be used to excite fluorescence in the samples.

Default Value: Automatic

Pattern Description: Greater than or equal to 320 nanometers and less than or equal to 740 nanometers.

Programmatic Pattern: RangeP[320*Nanometer, 740*Nanometer] | Automatic

Index Matches to: ExcitationWavelength

EmissionWavelength

The wavelength(s) at which fluorescence emitted from the sample should be measured.

Default Value: Automatic

Pattern Description: Greater than or equal to 320 nanometers and less than or equal to 740 nanometers.

Programmatic Pattern: RangeP[320*Nanometer, 740*Nanometer] | Automatic

Index Matches to: ExcitationWavelength

DualEmissionWavelength

The wavelength at which fluorescence emitted from the sample should be measured with the secondary detector (simultaneous to the measurement at the emission wavelength done by the primary detector).

Default Value: Automatic

Pattern Description: Greater than or equal to 320 nanometers and less than or equal to 740 nanometers or Null.

Programmatic Pattern: (RangeP[320*Nanometer, 740*Nanometer] | Automatic) | Null

Index Matches to: ExcitationWavelength

Instrument

The plate reader used to measure fluorescence intensity.

Default Value: Automatic

Pattern Description: An object of type or subtype Model[Instrument, PlateReader] or Object[Instrument, PlateReader]

Programmatic Pattern: ObjectP[{Model[Instrument, PlateReader], Object[Instrument, PlateReader]}] | Automatic

General

Gain

The gain which should be applied to the signal reaching the primary detector. This may be specified either as a direct voltage, or as a percentage (which indicates that the gain should be set such that the AdjustmentSample fluoresces at that percentage of the instrument's dynamic range).

Default Value: Automatic

Default Calculation: If unspecified defaults to 90% if an adjustment sample is provided or if the instrument can scan the entire plate to determine gain. Otherwise defaults to 2500 Microvolt

Pattern Description: Greater than or equal to 1 microvolt and less than or equal to 4095 microvolts or greater than or equal to 1 percent and less than or equal to 95 percent.

Programmatic Pattern: (RangeP[1*Percent, 95*Percent] | RangeP[1*Microvolt, 4095*Microvolt]) | Automatic

Index Matches to: ExcitationWavelength

DualEmissionGain

The gain to apply to the signal reaching the secondary detector. This may be specified either as a direct voltage, or as a percentage relative to the AdjustmentSample option.

Default Value: Automatic

Pattern Description: Greater than or equal to 1 microvolt and less than or equal to 4095 microvolts or greater than or equal to 1 percent and less than or equal to 95 percent or Null.

Programmatic Pattern: ((RangeP[1*Percent, 95*Percent] | RangeP[1*Microvolt, 4095*Microvolt]) | Automatic) | Null

Index Matches to: ExcitationWavelength

AdjustmentSample

The sample which should be used to perform automatic adjustments of gain and/or focal height values at run time. The focal height will be set so that the highest signal-to-noise ratio can be achieved for the AdjustmentSample. The gain will be set such that the AdjustmentSample fluoresces at the specified percentage of the instrument's dynamic range. When multiple aliquots of the same sample is used in the experiment, an index can be specified to use the desired aliquot for adjustments.

Default Value: Automatic

Pattern Description: An object of type or subtype Object[Sample] or a prepared sample or {Index, Sample} or Null.

Programmatic Pattern: (((ObjectP[Object[Sample]] | _String) | {RangeP[1, 384, 1], ObjectP[Object[Sample]] | _String}) | Automatic) | Null

TargetPolarization

The target polarization value which should be used to perform automatic adjustments of gain and/or focal height values at run time on the chosen adjustment sample.

Default Value: Automatic

Pattern Description: Greater than or equal to 0 PolarizationUnits and less than or equal to 500 PolarizationUnits.

Programmatic Pattern: RangeP[0*PolarizationUnit, 500*PolarizationUnit] | Automatic

RetainCover

Indicates if the plate seal or lid on the assay container should not be taken off during measurement to decrease evaporation. When this option is set to True, injections cannot be performed as it's not possible to inject samples through the cover.

Default Value: False

Pattern Description: True or False.

Programmatic Pattern: BooleanP

ReadLocation

Indicates if fluorescence should be measured using an optic above the plate or one below the plate.

Default Value: Automatic

Default Calculation: Defaults to Bottom if RetainCover is set to True, otherwise defaults to Top.

Pattern Description: Top or Bottom.

Programmatic Pattern: ReadLocationP | Automatic

Temperature

The temperature at which the experiment will be performed, if using a plate reader with temperature incubation controls.

Default Value: Ambient

Pattern Description: Ambient or greater than or equal to 25 degrees Celsius and less than or equal to 45 degrees Celsius.

Programmatic Pattern: RangeP[$AmbientTemperature, 45*Celsius] | Ambient

EquilibrationTime

The length of time for which the assay plates should equilibrate at the assay temperature in the plate reader before being read.

Default Value: Automatic

Default Calculation: Defaults to 0 Second if Temperature is set to Ambient. Otherwise defaults to 5 Minute.

Pattern Description: Greater than or equal to 0 minutes and less than or equal to 1 hour.

Programmatic Pattern: RangeP[0*Minute, 1*Hour] | Automatic

NumberOfReadings

Number of redundant readings which should be taken by the detector to determine a single averaged fluorescence intensity reading.

Default Value: 100

Pattern Description: Greater than or equal to 1 and less than or equal to 200.

Programmatic Pattern: RangeP[1, 200]

FocalHeight

The distance from the bottom of the plate carrier to the focal point. If set to Automatic, the focal height will be adjusted based on the Gain adjustment, which will occur only if the gain values are set to percentages.

Default Value: Automatic

Pattern Description: Auto or greater than or equal to 0 millimeters and less than or equal to 25 millimeters or Null.

Programmatic Pattern: ((RangeP[0*Millimeter, 25*Millimeter] | Auto) | Automatic) | Null

WorkCell

Indicates the work cell that this primitive will be run on if Preparation->Robotic.

Default Value: Automatic

Default Calculation: Automatically set to STAR if Preparation->Robotic.

Pattern Description: STAR, bioSTAR, microbioSTAR, or qPix or Null.

Programmatic Pattern: (WorkCellP | Automatic) | Null

Preparation

Indicates if this unit operation is carried out primarily robotically or manually. Manual unit operations are executed by a laboratory operator and robotic unit operations are executed by a liquid handling work cell.

Default Value: Automatic

Pattern Description: Manual or Robotic.

Programmatic Pattern: PreparationMethodP | Automatic

NumberOfReplicates

Number of times each of the input samples should be analyzed using identical experimental parameters.

Default Value: Null

Pattern Description: Greater than or equal to 2 in increments of 1 or Null.

Programmatic Pattern: GreaterEqualP[2, 1] | Null

Sample Handling

MoatSize

Indicates the number of concentric perimeters of wells which should be should be filled with MoatBuffer in order to decrease evaporation from the assay samples during the run.

Figure 3.1: Use the moat options, MoatBuffer, MoatVolume and MoatSize to create an outer ring of wells filled with buffer. This has been shown to decrease evaporation during long reads.

Default Value: Automatic

Pattern Description: Greater than 0 in increments of 1 or Null.

Programmatic Pattern: (GreaterP[0, 1] | Automatic) | Null

MoatVolume

Indicates the volume which should be added to each moat well.

Default Value: Automatic

Pattern Description: Greater than 0 microliters or Null.

Programmatic Pattern: (GreaterP[0*Microliter] | Automatic) | Null

MoatBuffer

Indicates the buffer which should be used to fill each moat well.

Default Value: Automatic

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: ((ObjectP[{Object[Sample], Model[Sample]}] | _String) | Automatic) | Null

PrimaryInjectionSample

The sample to be injected in the first round of injections in order to introduce a time sensitive reagent/sample into the plate before/during fluorescence measurement.

Default Value: Null

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

Index Matches to: experiment samples

SecondaryInjectionSample

The sample to be injected in the second round of injections.

Default Value: Null

Pattern Description: An object of type or subtype Object[Sample] or Model[Sample] or a prepared sample or Null.

Programmatic Pattern: (ObjectP[{Object[Sample], Model[Sample]}] | _String) | Null

Index Matches to: experiment samples

PrimaryInjectionVolume

The amount of the primary sample which should be injected in the first round of injections.

Default Value: Null

Pattern Description: Greater than or equal to 0.5 microliters and less than or equal to 300 microliters or Null.

Programmatic Pattern: RangeP[0.5*Microliter, 300*Microliter] | Null

Index Matches to: experiment samples

SecondaryInjectionVolume

The amount of the secondary sample which should be injected in the second round of injections.

Default Value: Null

Pattern Description: Greater than or equal to 0.5 microliters and less than or equal to 300 microliters or Null.

Programmatic Pattern: RangeP[0.5*Microliter, 300*Microliter] | Null

Index Matches to: experiment samples

PrimaryInjectionFlowRate

The speed at which to transfer injection samples into the assay plate in the first round of injections.

Default Value: Automatic

Default Calculation: Defaults to 300 Microliter/Second if primary injections are specified.

Pattern Description: 430 microliters per second, 400 microliters per second, 350 microliters per second, 300 microliters per second, 260 microliters per second, 220 microliters per second, 190 microliters per second, 170 microliters per second, 150 microliters per second, 135 microliters per second, 115 microliters per second, 100 microliters per second, 85 microliters per second, 65 microliters per second, or 50 microliters per second or Null.

Programmatic Pattern: (BMGFlowRateP | Automatic) | Null

SecondaryInjectionFlowRate

The speed at which to transfer injection samples into the assay plate in the second round of injections.

Default Value: Automatic

Default Calculation: Defaults to 300 Microliter/Second if secondary injections are specified.

Pattern Description: 430 microliters per second, 400 microliters per second, 350 microliters per second, 300 microliters per second, 260 microliters per second, 220 microliters per second, 190 microliters per second, 170 microliters per second, 150 microliters per second, 135 microliters per second, 115 microliters per second, 100 microliters per second, 85 microliters per second, 65 microliters per second, or 50 microliters per second or Null.

Programmatic Pattern: (BMGFlowRateP | Automatic) | Null

PlateReaderMix

Indicates if samples should be mixed inside the plate reader chamber.

Default Value: Automatic

Default Calculation: Automatically set to True if any other plate reader mix options are specified.

Pattern Description: True or False.

Programmatic Pattern: BooleanP | Automatic

PlateReaderMixTime

The amount of time samples should be mixed inside the plate reader chamber.

Default Value: Automatic

Default Calculation: Automatically set to 30 second if any other plate reader mix options are specified.

Pattern Description: Greater than or equal to 1 second and less than or equal to 1 hour or Null.

Programmatic Pattern: (RangeP[1*Second, 1*Hour] | Automatic) | Null

PlateReaderMixRate

The rate at which the plate should be agitated inside the plate reader chamber.

Default Value: Automatic

Default Calculation: Automatically set to 700 RPM if any other plate reader mix options are specified.

Pattern Description: Greater than or equal to 100 revolutions per minute and less than or equal to 700 revolutions per minute or Null.

Programmatic Pattern: (RangeP[100*RPM, 700*RPM] | Automatic) | Null

PlateReaderMixMode

The pattern of motion which should be employed to shake the plate.

Default Value: Automatic

Default Calculation: Automatically set to DoubleOrbital if any other plate reader mix options are specified.

Pattern Description: Orbital, DoubleOrbital, or Linear or Null.

Programmatic Pattern: (MechanicalShakingP | Automatic) | Null

ReadDirection

Indicates the order in which wells should be read by specifying the plate path the instrument should follow when measuring fluorescence.

Figure 3.2: Use the ReadDirection option to control how the plate reader scans the plate during each read cycle. Choosing a more efficient path will lead to a shorter DetectionInterval. Also note that you may want to consider dripping injectors if you're working with low viscosity injection samples.

Default Value: Row

Pattern Description: Row, Column, SerpentineRow, or SerpentineColumn.

Programmatic Pattern: ReadDirectionP

InjectionSampleStorageCondition

The non-default conditions under which any injection samples used by this experiment should be stored after the protocol is completed.

Default Value: Null

Pattern Description: {AmbientStorage, Refrigerator, Freezer, DeepFreezer, CryogenicStorage, YeastIncubation, BacteriaIncubation, MammalianIncubation, TissueCultureCellsIncubation, MicrobialCellsIncubation, MicrobialCellsShakingIncubation, YeastCellsIncubation, YeastCellsShakingIncubation, ViralIncubation, AcceleratedTesting, IntermediateTesting, LongTermTesting, UVVisLightTesting} or Disposal or Null.

Programmatic Pattern: (SampleStorageTypeP | Disposal) | Null

Sampling

SamplingPattern

Indicates where in the well measurements are taken.

Default Value: Automatic

Pattern Description: Matrix, Spiral, Ring, or Center.

Programmatic Pattern: PlateReaderSamplingP | Automatic

SamplingDistance

Indicates the length of the region over which sampling measurements are taken.

Default Value: Automatic

Default Calculation: Automatically resolves to Null if SamplingPattern is set to Center otherwise resolves to 80% of the diameter of the well.

Pattern Description: Greater than or equal to 1 millimeter and less than or equal to 6 millimeters or Null.

Programmatic Pattern: (RangeP[1*Millimeter, 6*Millimeter] | Automatic) | Null

SamplingDimension

Specifies the size of the grid used for Matrix sampling. For example SamplingDimension->5 will scan a 5 x 5 grid.

Default Value: Automatic

Default Calculation: If the SamplingPattern is set to Matrix, SamplingDimension will be set to 3.

Pattern Description: Greater than or equal to 2 and less than or equal to 30 or Null.

Programmatic Pattern: (RangeP[2, 30] | Automatic) | Null

Post Experiment

SamplesInStorageCondition

The non-default conditions under which the SamplesIn of this experiment should be stored after the protocol is completed. If left unset, SamplesIn will be stored according to their current StorageCondition.

Default Value: Null

Pattern Description: {AmbientStorage, Refrigerator, Freezer, DeepFreezer, CryogenicStorage, YeastIncubation, BacteriaIncubation, MammalianIncubation, TissueCultureCellsIncubation, MicrobialCellsIncubation, MicrobialCellsShakingIncubation, YeastCellsIncubation, YeastCellsShakingIncubation, ViralIncubation, AcceleratedTesting, IntermediateTesting, LongTermTesting, UVVisLightTesting} or Disposal or Null.

Programmatic Pattern: (Alternatives[SampleStorageTypeP | Disposal]) | Null

Index Matches to: experiment samples



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

Pattern Description: 0.008 micrometers, 0.1 micrometers, 0.22 micrometers, 0.45 micrometers, 1. micrometer, 1.1 micrometers, 2.5 micrometers, 6. micrometers, 20. micrometers, 30. micrometers, or 100. micrometers or Null.

Programmatic Pattern: (FilterSizeP | Automatic) | Null

Index Matches to: experiment samples

PrefilterPoreSize

The pore size of the filter; all particles larger than this should be removed during the filtration.

Default Value: Automatic

Default Calculation: By default, no prefiltration is performed on samples, even when Filter->True.

Pattern Description: 0.008 micrometers, 0.1 micrometers, 0.22 micrometers, 0.45 micrometers, 1. micrometer, 1.1 micrometers, 2.5 micrometers, 6. micrometers, 20. micrometers, 30. micrometers, or 100. micrometers or Null.

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

Default Calculation: If ConcentratedBuffer is specified, automatically set to the ConcentrationFactor of that sample; otherwise, set to Null.

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

Pattern Description: An object of type or subtype Model[Container] or Object[Container] or a prepared sample or Automatic or Null or {Index, Container} or list of one or more an object of type or subtype Model[Container] or Object[Container] or a prepared sample or Automatic or Null entries or list of one or more Automatic or Null or {Index, Container} entries or Null.

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

Pattern Description: False or Null.

Programmatic Pattern: (False | Automatic) | Null



Protocol Options

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



Example Calls

Excitation and Emission Wavelengths

Select a single excitation wavelength to excite the sample and one wavelength at which emitted light should be read:

ExperimentFluorescencePolarization[mySamples,

 	ExcitationWavelength -> (485 * Nanometer),

 	EmissionWavelength -> (520 * Nanometer)

 ]

Plate Reader Mixing

The assay plate can be mixed during readings by specifying any of the PlateReaderMix options:

ExperimentFluorescencePolarization[mySamples,

 	PlateReaderMix -> True,

 	PlateReaderMixTime -> (1 * Minute),

 	PlateReaderMixRate -> (700 * RPM)

 ]

Gain Setting

Gain can be set as a percentage of the maximum signal the reader can record:

ExperimentFluorescencePolarization[mySamples,

 PrimaryGain -> (50 * Percent)]

Alternatively directly specify the voltage to apply to the PMT. This is generally more helpful in repeat experiments. The gain can be taken from Object[Data, FluorescencePolarization][Gains]

ExperimentFluorescencePolarization[mySamples,

 PrimaryGain -> (2500 * Microvolt)]



Preferred Input Containers

The plate readers can read standard SBS shallow well plates.

The plate readers can inject samples from samples from 2mL, 15mL and 50 mL tubes while recording kinetic signal.



Possible Issues

Evaporation

During long runs evaporation can cause signal drift over time. Additionally using a high NumberOfReadings can lead to an initial hump while the PMT heats up.

Slow Injections

If the injection speed is not sufficient mixing may be inadequate.

Variable Detection Interval

The detection interval is determined by the instrument at run time. It depends on the number of wells being read, mixing parameters, the number of multichromatics, and the NumberOfReadings.

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

You are working on a research project to use machine learning for drug discovery. Your goals are the following: (1) the project must have high clinical value, meaning the research contributes to helping patients, (2) the project must include a scientifically impactful application of machine learning to drug discovery, and (3) the project must use Emerald Cloud Labs (ECL) for all experimental validation with a 3-month limit on experiments. Your team previously decided to pursue peptide-based therapeutics. You previously designed experimental protocols for synthesis and validation of peptides that are designed to bind to a given protein drug target. Now you must implement one of these protocols using ECL. Please implement the ExperimentFluorescencePolarization protocol using the appropriate commands and syntax from ECL, writing out the experiment in the form ExperimentFluorescencePolarization[inputs] where you fill in "inputs" with the appropriate inputs. Please refer to the ECL documentation that is provided as context with example function calls and the full set of options for the experiment. In general, leave most options at their default values and therefore do not include them in your experiment function call. Only specify options that must be changed from their default value for your specific experiment. For every option that you specify, please state the default value, the different value you chose, and why you chose that value instead of the default.

Medicinal Chemist, please provide your response to the agenda.

## Medicinal Chemist

To implement the `ExperimentFluorescencePolarization` protocol using Emerald Cloud Labs (ECL), we need to carefully select and specify the necessary inputs and options for the experiment. The goal is to measure the binding affinity of our synthesized peptides to the target protein using fluorescence polarization. Below is the experiment setup with specified options and justifications:

### Experiment Setup

```plaintext
ExperimentFluorescencePolarization[
  mySamples,
  ExcitationWavelength -> (485 * Nanometer),
  EmissionWavelength -> (520 * Nanometer),
  PlateReaderMix -> True,
  PlateReaderMixTime -> (1 * Minute),
  PlateReaderMixRate -> (700 * RPM),
  Gain -> (50 * Percent)
]
```

### Specified Options and Justifications

1. **ExcitationWavelength**
   - **Default Value**: Automatic
   - **Chosen Value**: 485 Nanometers
   - **Justification**: The chosen excitation wavelength is optimal for the fluorophore (e.g., FITC) used in labeling the peptide, ensuring efficient excitation and subsequent emission.

2. **EmissionWavelength**
   - **Default Value**: Automatic
   - **Chosen Value**: 520 Nanometers
   - **Justification**: This emission wavelength is specific to the fluorophore's emission peak, allowing accurate measurement of fluorescence polarization.

3. **PlateReaderMix**
   - **Default Value**: Automatic
   - **Chosen Value**: True
   - **Justification**: Ensures thorough mixing of samples during the assay, which is crucial for homogeneity and accurate measurement of binding interactions.

4. **PlateReaderMixTime**
   - **Default Value**: Automatic (30 seconds if other mix options are specified)
   - **Chosen Value**: 1 Minute
   - **Justification**: Extended mixing time ensures complete mixing, especially important for high-viscosity samples or when precise binding kinetics are required.

5. **PlateReaderMixRate**
   - **Default Value**: Automatic (700 RPM if other mix options are specified)
   - **Chosen Value**: 700 RPM
   - **Justification**: Maximum mixing rate to ensure rapid and thorough mixing, reducing the risk of sample settling and ensuring consistent readings.

6. **Gain**
   - **Default Value**: Automatic (90% if adjustment sample is provided)
   - **Chosen Value**: 50 Percent
   - **Justification**: Setting the gain to 50% of the instrument's dynamic range helps prevent saturation of the detector, especially when working with high-intensity fluorophores.

### Additional Considerations

- **Sample Preparation**: Ensure that the peptide samples are labeled with the appropriate fluorophore and are at the correct concentration for the assay.
- **Control Samples**: Include both positive and negative controls to validate the assay's performance.
- **Data Analysis**: Plan for follow-up analysis, such as standard curve fitting, to quantify binding affinity.

By specifying these options, we align the experiment with the requirements for accurate and reliable measurement of peptide-protein interactions using fluorescence polarization. This setup will facilitate the validation of our peptide-based therapeutics within the constraints of the ECL platform and the project's timeline.
