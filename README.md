# pandasfruit

## Summary
Takes in a pandas dataframe and returns a string containing markdown format where the width of the markdown text is more narrow and is suitable for printing. The more narrow table can fit on a printed page, such as a PDF generated from a Jupyter notebook.

Takes in an optional width parameter (number of characters) and will make the resulting markdown this wide. Else will use a default width of 115.

Also will use a default dictionary of words/abbreviations to shorten column names using the abbreviations instead of the original words. Alternatively, a  user-defined dictionary may be passed in. Pass in empty dictionary to do no replacements.

## Processing
To achieve the more-narrow markdown version of the df, first column names are shortened using the default abbreviations dictionary (or the optional user-provided dictionary). Keywords in column names are replaced with abbreviations. Note that column names may contain words separated by either underscores or spaces.

If, after wrapping column names, the width of the markdown is still greater than the desired markdown width, the columns are iteratively wrapped to increasingly shorter widths until the desired width of the markdown is achieved.

## Installation
pip install pandasfruit

## Usage
```python
import pandas as pd
from pandasfruit import pandasfruit
```

```python
x = pd.DataFrame(
    {
        'c foobar person number clean': [
            '00000001',
            '00000002',
            '00000003',
            '00000004',
            '00000005',
            '00000006',
            '00000007',
            '00000008'
        ],
        
        'c foobar first name clean': [
            'Eduard',
            'Andriel',
            'Faris',
            'Shaye',
            'Rodney',
            'Arledge',
            'Cory',
            'Madison'
        ],
        
        'c foobar last name clean': [
            'Davis',
            'Bell',
            'Russell',
            'Fisher',
            'Wilson',
            'Campbell',
            'Collins',
            'Thomas'
        ],
        
        'c _foobar_home_street_address_1_clean': [
        
            '1234 Maple Street REALLY REALLY REALLY SUPER REAL LONG '
            'STREET MORE MORE MORE WORDS SOME MORE',
            '5678 Oakwood Avenue',
            '910 Willow Lane',
            '1122 Elm Drive',
            '1314 Cedar Boulevard',
            '1516 Pine Court',
            '1718 Birch Road',
            '1920 Juniper Place REALLY REALLY REALLY SUPER DUPER LONG '
            'APARTMENT NAME EVEN MORE WORDS HERE OK SOME MORE'
        ],

        'c foobar home street address 2 clean': [
            'Apartment 200',
            'Suite 6 MORE MORE MORE AND EVEN MORE WORDS AND ADDING SOME '
            'MORE WORDS AND HERE ARE EVEN SOME MORE AND EVEN MORE WORDS '
            'ARE ADDED HERE OK',
            'Apt. 2',
            'Apartment 4021',
            '2nd Floor',
            'Unit C',
            'Apt. 3',
            'Downstairs'
        ]
    }
)
```
```python
print(x.to_markdown(tablefmt='grid'))
```

![](https://github.com/bol001/pandasfruit/assets/61277863/42abe0c8-4c92-41c3-9614-70c8e2444256)

```python
x_for_display = pandasfruit.df_to_fitted_markdown(x)

print(x_for_display)
```

![](https://github.com/bol001/pandasfruit/assets/61277863/1ef6b638-53ad-4387-ae74-9c39f73fdf6d)

```python
x_for_display = pandasfruit.df_to_fitted_markdown(x, width=80, abbreviations={'foo_bar': 'fb', 'baz ham': 'baz h'})
```