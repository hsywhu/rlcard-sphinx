# rlcard-sphinx
Source files for generating rlcard website http://rlcard.org using sphinx. 

## development
- Install python dependencies: `sphinx-rtd-theme` (this would also install sphinx), `myst-parser`
- Copy the cloned repo over to `rlcard/docs`
- Update the rst and md documents under `sphinx/source`
- Run `make html`
- Deploy the `html` folder of `build` to the website