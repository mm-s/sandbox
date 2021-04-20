Business requires a solution implying minimal cooperation with customer,
who would supply a public key, then receive a tx payload to sign and announce.


=======================================
I patched symbol-bootstrap as a way to obtain the tx payload.
use a patched version of symbol-bootstrap before continuing.
execute :
cd symbol-bootstrap
git patch symbol-bootstrap.patch

If this ends up working the change in bootstrap must be accomodated.
=========================================

Custodial bz:
./serverman

Customer
./climan



