---
layout: post
title: FreeNAS Disable ACPI on boot
date: 2010-04-04
---

I ran into a problem on a particular computer where FreeNAS did not like how the bios was reporting the temperature. FreeNAS would constantly prompt that the temperature was "absurd". I found that booting to option two from the boot menu, disabled ACPI, would fix the problem. The next problem was locating the file which controlled this. To disable ACPI on boot  

Edit:  
`/cf/boot/device.hints`  
  
Add:  
`hint.acpi.0.disabled="1"`  
  
Now reboot and ACPI should be disabled by default. As far as I can tell, this still uses option 1 as the default but forces it to not load ACPI.  

**Update:** This was tested on FreeNAS, version 0.69 , 0.7.1 and 0.7.2
