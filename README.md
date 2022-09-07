# python-mssev

This library contains several utilities and scores commonly used in multiple
sclerosis studies.

## Installation

```shell
pip install mssev
```

## Usage

```python
import mssev as ms
```

### Calculating irreversible disability

If you want to calculate some irreversible disability score (such as the EDSS),
you can do so with the following code:

```python
followups['Irr_EDSS'] = ms.irreversible_ds(followups,
                                           id='ID', ds='EDSS', date='Date',
                                           min_period=np.timedelta64(6, 'M'))
```

### Calculating the MSSS

The Multiple Sclerosis Severity Score (MSSS) is obtained by normalising the
Expanded Disability Status Scale (EDSS) score for disease duration and has been
a valuable tool in cross-sectional studies. You can read the original article
[here](https://doi.org/10.1212/01.WNL.0000156155.19270.F8).

You can calculate the MSSS for every patient with the following:

```python
patients['MSSS'] = ms.global_msss(patients, ds='Irreversible EDSS', duration='Duration')
```

If you want to calculate the MSSS for each follow-up assessment, you can do so
like this:

```python
followups['MSSS'] = ms.global_msss(followups, ds='EDSS', duration='Duration')
```

### Calculating the ARMSS

The ARMSS (Age-Related Multiple Sclerosis Severity) score is the result of
standardizing the EDSS by age. Using age for the calculation instead of disease
duration offers several advantages, not least of which are its availability,
ease of measurement and absence of bias.

If you want more information on the advantages of this score, I recommend that
you read the original article, available [here](https://doi.org/10.1177%2F1352458517690618).

You can easily calculate the ARMSS for every patient like this:

```python
patients['ARMSS'] = ms.global_armss(patients, ds='EDSS', age='Age')
```

Or alternatively, you can calculate it for every follow-up assessment like this:

```python
followups['ARMSS'] = ms.global_armss(followups, ds='EDSS', age='Age')
```