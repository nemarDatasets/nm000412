# ECoG hemispheric asymmetry during reaching (Merrick et al. 2022): authors' 1000 Hz exports

Intracranial recordings from **six patients with intractable epilepsy** implanted with subdural grids, three with
left-hemisphere implants (L1-L3) and three with right-hemisphere implants (R4-R6). They were recorded at the University
of California, Irvine, the University of California, San Francisco Medical Center and California Pacific Medical
Center, San Francisco, two patients per site. Patients performed an **instructed-delay reaching task** on a touchscreen,
with two blocks of 40 trials for each arm, in counterbalanced order. Re-packaged from the authors' public release
(Zenodo record [4761390](https://doi.org/10.5281/zenodo.4761390), "ECoG_Hemispheric_Asymmetry_dataset", CC-BY-4.0).

Reference article: Merrick CM, Dixon TC, Breska A, Lin J, Chang EF, King-Stephens D, Laxer KD, Weber PB, Carmena J,
Knight RT, Ivry RB. *Left hemisphere dominance for bilateral kinematic encoding in the human brain.* eLife 11:e69977
(2022). https://doi.org/10.7554/eLife.69977. Code: https://github.com/cmerrick15/Asymmetry_ECoG_dataset

## This is a derivative dataset
The neural arrays in the release are the authors' exports at **1000 Hz**. The paper says UCI recorded at 5000 Hz
(Nihon Kohden), UCSF at 3052 Hz (Tucker Davis Technologies) and CPMC at 1000 Hz (Nihon Kohden). The UCI and UCSF data
were low-pass filtered at 500 Hz and downsampled to 1000 Hz. Channels that the release metadata lists as bad
(`SDATA.metadata.bad_electrodes`) are already absent from the arrays. The release does not say whether its exports also
include the paper's common-average reference and 60/120/180 Hz notch filters. The dataset is therefore labelled
`DatasetType: derivative`. The packaging itself changes no values.

## Layout
- `sub-L1`...`sub-R6` = release patient IDs. `task-reach`, `acq-lefthand` / `acq-righthand` = arm used,
  `run-1` / `run-2` = block.
- `*_ieeg.vhdr`: `SDATA.data` (float32 BrainVision; values are the stored float64 values rounded to float32). Channel
  names are as in `SDATA.info.channel_labels`. The release does not give units; the magnitudes differ by site (see
  `task-reach_channels.json`).
- `*_recording-kinematics_physio.tsv.gz`: the release `kin_mat` (position, speed, x, y, z, theta, phi) at 100 Hz. The
  paper estimated the movement profiles from the button and touch times. `StartTime` 0 assumes that the kinematics start
  with the neural export: the lengths agree at 10:1 to within one sample, but the release does not state the alignment.
- The release holds no trial events: the `SDATA.events` structures are empty, and R5's is an undocumented MATLAB table
  object. The photodiode and microswitch analog channels (`SDATA.analog`, 4 channels at 24414 Hz for UCSF, 5000 Hz for
  UCI L3 and 1000 Hz for CPMC; absent for R4) remain only in the source files in `sourcedata/`.
- `participants.tsv`: age and handedness from Table 1 for L1-L3. Table 1 names the right-hemisphere patients R1-R3
  (ages 26, 32 and 34, all right-handed), but the release uses R4-R6 and does not state the correspondence, so R4-R6 are
  `n/a`. Sex is given only at group level (two of six female). `recording_site` is inferred from the release session
  codes (EC = UCSF, IR = UCI, CP = CPMC) and the analog sampling rates, which matches the paper's two patients per site.
- Channel types: the release types electrodes only for L1 and L2 (grid / strip). Elsewhere all channels are typed ECOG
  (see `task-reach_channels.json`). There are no electrode coordinates in the release. `electrodes.tsv` lists names with
  `n/a` coordinates.

## Source files
`sourcedata/zenodo-4761390/` holds all 48 release `.mat` files: the neural `SDATA` structures, including the analog
channels, the empty events, `info.id` session codes and, for R4 right-hand block 1, an extra `data_ref` array. It also
holds the kinematics files and the Zenodo record metadata. The only change is that the MATLAB header text "Created on"
(file export date, 2019-2021) has its weekday and day masked. The provenance JSON gives the SHA-256 of each file before
and after masking.

## License

CC-BY-4.0

## Additional metadata and localisation (added 2026-10-08)

Compiled after the upload from the article, its supplement and the source deposit (each statement names its source). Text and sidecar metadata only; no data file was changed.

**Recording system.** Nihon Kohden at UCI (128 ch, 5000 Hz) and CPMC (128 ch, 1000 Hz); Tucker Davis Technologies at UCSF (128 ch, 3052 Hz); signals not at 1000 Hz were low-pass filtered at 500 Hz and downsampled to 1000 Hz (paper Methods). Deposit SDATA.info.sampling_rate = 1000 for all six; L1/L2 also carry analog_sr 24414.0625 (TDT analog rate).

**Reference scheme.** Common average reference applied in the paper's preprocessing; notch 60/120/180 Hz (paper Methods). Whether the deposited SDATA.data is pre- or post-CAR is not stated (n/a).

**Electrode types.** Subdural grids and strips; spacing 1 cm in four patients and 4 mm in the other two (paper "Electrode localization"). 752 electrodes in total, 82 removed for noise and 5 for epileptic activity -> 665 analysed (paper Methods).

**Localisation.** Electrode locations visualised on each patient's 3D cortical reconstruction by co-registering post-operative CT to pre-operative MRI (Stolk et al. 2018 pipeline); each electrode was categorised with the Desikan-Killiany parcellation; pooled proportions are shown per hemisphere in Figure 2-figure supplement 1 (premotor: superior frontal, caudal middle frontal, pars opercularis; sensorimotor: pre-/post-central; parietal: supramarginal, superior parietal, inferior parietal; 70% of electrodes in these parcels). Per-electrode coordinates/labels are not deposited.

### Regions per participant (as published; no coordinates exist)

| participant | region (as stated) | hemisphere | contacts | source |
|---|---|---|---|---|
| cohort-left(L1-L3) | Superior frontal; Caudal middle frontal; Opercularis | left | n/a | doi:10.7554/eLife.69977, Figure 2-figure supplement 1 (premotor group |
| cohort-left(L1-L3) | Pre-central; Post-central | left | n/a | doi:10.7554/eLife.69977, Figure 2-figure supplement 1 (sensorimotor) |
| cohort-left(L1-L3) | Supra marginal; Superior parietal; Inferior parietal | left | n/a | doi:10.7554/eLife.69977, Figure 2-figure supplement 1 (parietal) |
| cohort-right(R4-R6) | Superior frontal; Caudal middle frontal; Opercularis | right | n/a | doi:10.7554/eLife.69977, Figure 2-figure supplement 1 |
| cohort-right(R4-R6) | Pre-central; Post-central | right | n/a | doi:10.7554/eLife.69977, Figure 2-figure supplement 1 |
| cohort-right(R4-R6) | Supra marginal; Superior parietal; Inferior parietal | right | n/a | doi:10.7554/eLife.69977, Figure 2-figure supplement 1 |
