# On-Premises Server Hardware Specs

To support 100 developers doing typical development \(periodic spikes\), Maana recommends, at minimal, a configuration of 4 servers.  

{% hint style="info" %}
Preference is: more RAM, more disk, and more CPU \(in this order\).
{% endhint %}

## Example

* 4 servers with 64GB RAM + 1TB SSD + Quad Processor Xeon \(multicore\) 2.8+ Ghz would be sufficient.
* Base software: Ubuntu 16.4+, Docker, Python3
* Custom software \(we install\): Ansible, GlusterFS
* If Spark or TensorFlow is desired, or other computational environments for time series or deep learning, then additional, dedicated \(specialized\) clusters would be needed \(i.e., optimized for Hadoop, NVIDIA GPUs\).

