# ethash
Ethash Python spec code

Ethash (Ethereum Proof-of-Work algorythm) Python spec code from https://github.com/ethereum/wiki/wiki/Ethash with some changes. For those who want to try to understand how Ethereum PoW works without delving into low-level programming.

Runs on Python 2, fails on Python 3.

Usage:
  python ethash.py
  
  
Right now doesn't accept command line arguments.

Changes in comparison with Wiki version:
* Added a main function to prepare all variables and launch mining
* Added some output to 'mine' function
* Commented out reversing of padded target: the reason is that reversing is being made by the call to 'encode_int' (https://github.com/lukovkin/ethash/blob/master/ethash.py#L20). May be it's wrong but otherwise target gets larger with difficulty increase, which leads to the behavior when 'mine' finds solution faster if we increase difficulty, which seems to be wrong.
* Use only 'result' from the output of the 'hashimoto' function - https://github.com/lukovkin/ethash/blob/master/ethash.py#L906.
* Call 'decode_int' for the result and target in the comparison https://github.com/lukovkin/ethash/blob/master/ethash.py#L906) - may be it's not required?
* Encode nonce to byte array (https://github.com/lukovkin/ethash/blob/master/ethash.py#L863), otherwise we get an exception here - https://github.com/lukovkin/ethash/blob/master/ethash.py#L864.

Notes:
* I'm not sure that changes made to the algo are correct, advise needed
* Preparation of the full dataset takes a few hours on my box (in a single thread). Multiprocessing is to be used to speed up.
