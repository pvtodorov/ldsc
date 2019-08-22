###################################### The problem ######################################
munge_sumstats.py must be run with pandas 0.20.x
In addition, pandas 0.20.x does not work will newer versions of numpy. 
See environment_munge.yml for details.

To munge GWAS data, use the environment_munge.yml env:
conda env create -f ldsc/environment_munge.yml
conda activate ldsc_munge
python munge_sumstats.py ....

Tested for both munge_sumstats.py and mtag_munge.py

###################################### Google Forum ######################################

REF: https://groups.google.com/forum/#!msg/ldsc_users/9Mxw4vAB2l8/Muc_vtmYAwAJ
Hi Max,
Yes, pandas versioning is almost certainly the issue here. My understanding is this error occurs with pandas 0.21, but works correctly if you revert to e.g. 0.20.1.
Cheers,
Raymond



@@@@@@@@@@@@@@@@@@ Error when using e.g. pandas 0.23.4 @@@@@@@@@@@@@@@@@@
Reading list of SNPs for allele merge from /projects/timshel/sc-genetics/ldsc/data/w_hm3.snplist
Read 1217311 SNPs for allele merge.
Reading sumstats from /projects/timshel/sc-genetics/sc-genetics/data/gwas_sumstats_raw/INSOMNIA_Jansen2018/Insomnia_sumstats_Jansenetal.txt.gz into memory 5000000 SNPs at a time.
... done
Read 10862567 SNPs from --sumstats file.
Removed 9698237 SNPs not in --merge-alleles.
Removed 0 SNPs with missing values.
Removed 0 SNPs with INFO <= 0.9.
Removed 27921 SNPs with MAF <= 0.01.
Removed 0 SNPs with out-of-bounds p-values.
Removed 87 variants that were not SNPs or were strand-ambiguous.
1136322 SNPs remain.
Removed 0 SNPs with duplicated rs numbers (1136322 SNPs remain).
Removed 0 SNPs with N < 257688.666667 (1136322 SNPs remain).
Median value of OR was 1.0, which seems sensible.
Removed 120 SNPs whose alleles did not match --merge-alleles (1136202 SNPs remain).

ERROR converting summary statistics:

Traceback (most recent call last):
  File "/projects/timshel/sc-genetics/ldsc/ldsc/munge_sumstats.py", line 707, in munge_sumstats
    dat = allele_merge(dat, merge_alleles, log)
  File "/projects/timshel/sc-genetics/ldsc/ldsc/munge_sumstats.py", line 445, in allele_merge
    dat.loc[~jj, [i for i in dat.columns if i != 'SNP']] = float('nan')
  File "/tools/anaconda/3-4.4.0/envs/py27_anaconda3_PT170705/lib/python2.7/site-packages/pandas/core/indexing.py", line 188, in __setitem__
    indexer = self._get_setitem_indexer(key)
  File "/tools/anaconda/3-4.4.0/envs/py27_anaconda3_PT170705/lib/python2.7/site-packages/pandas/core/indexing.py", line 166, in _get_setitem_indexer
    return self._convert_tuple(key, is_setter=True)
  File "/tools/anaconda/3-4.4.0/envs/py27_anaconda3_PT170705/lib/python2.7/site-packages/pandas/core/indexing.py", line 247, in _convert_tuple
    idx = self._convert_to_indexer(k, axis=i, is_setter=is_setter)
  File "/tools/anaconda/3-4.4.0/envs/py27_anaconda3_PT170705/lib/python2.7/site-packages/pandas/core/indexing.py", line 1327, in _convert_to_indexer
    .format(mask=objarr[mask]))
KeyError: '[-2 -2 -2 ... -1 -1 -2] not in index'



@@@@@@@@@@@@@@@@@@ Error when using newest pandas  @@@@@@@@@@@@@@@@@@

.....
Removed 0 SNPs whose alleles did not match --merge-alleles (1019865 SNPs remain).

ERROR converting summary statistics:

Traceback (most recent call last):
  File "/projects/timshel/sc-genetics/mtag/mtag_munge.py", line 887, in munge_sumstats
    dat = allele_merge(dat, merge_alleles)
  File "/projects/timshel/sc-genetics/mtag/mtag_munge.py", line 596, in allele_merge
    dat.loc[~jj, [i for i in dat.columns if i != 'SNP']] = float('nan')
  File "/projects/timshel/sc-genetics/mtag/mtag_munge.py", line 596, in allele_merge
    dat.loc[~jj, [i for i in dat.columns if i != 'SNP']] = float('nan')
  File "/tools/anaconda/envs/djw472/py2_PT/lib/python2.7/site-packages/pandas/core/indexing.py", line 189, in __setitem__
    indexer = self._get_setitem_indexer(key)
  File "/tools/anaconda/envs/djw472/py2_PT/lib/python2.7/site-packages/pandas/core/indexing.py", line 167, in _get_setitem_indexer
    return self._convert_tuple(key, is_setter=True)
  File "/tools/anaconda/envs/djw472/py2_PT/lib/python2.7/site-packages/pandas/core/indexing.py", line 248, in _convert_tuple
    idx = self._convert_to_indexer(k, axis=i, is_setter=is_setter)
  File "/tools/anaconda/envs/djw472/py2_PT/lib/python2.7/site-packages/pandas/core/indexing.py", line 1354, in _convert_to_indexer
    return self._get_listlike_indexer(obj, axis, **kwargs)[1]
  File "/tools/anaconda/envs/djw472/py2_PT/lib/python2.7/site-packages/pandas/core/indexing.py", line 1161, in _get_listlike_indexer
    raise_missing=raise_missing)
  File "/tools/anaconda/envs/djw472/py2_PT/lib/python2.7/site-packages/pandas/core/indexing.py", line 1246, in _validate_read_indexer
    key=key, axis=self.obj._get_axis_name(axis)))
KeyError: u"None of [Int64Index([-1, -1, -1, -1, -1, -1, -1, -2, -2, -1,\n            ...\n            -1, -1, -1, -1, -2, -2, -2, -1, -1, -1],\n           dtype='int64', length=1217311)] are in the [index]"
