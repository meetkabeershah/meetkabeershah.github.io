---
layout: post
title: Setting Up Perfmon for SQL Server Tuning
---

Performance Monitor, or Perfmon, measures performance statistics on a regular interval, and saves those stats in a file.

To set it up for SQL Server, do the below steps:

 - Open perfmon from the run
 - Expand Data Collector Sets
 - Right click **User Defined**
 - Click **New** -> **Data Collector Set**
 - Give it a name
 - Click Create manually

![Manually create Data Collector Set](https://lh3.googleusercontent.com/sbmD1ZIJ3FU3OfbH2JzdknCIHTT1UPFxSIfCsHy1ldZOf_QLpBe3ffmS-TAuf3kgwoJqop66r7MGBuBN0_-F63_RglNDkq8YRBE-feuX8N_RoOInYUFCbwjHkmzoMPOVpGNxv6xslF9ZD0jkzt51sKC9rcTyCM-acf0y0x3YSEOBo5OePkqkKFWCzRVRtF_TTsYWfAEPKXyjjKf1kIza43qBP4mvx7X3M9n0RHseJUyL9T10SL8U9FrwzOgeIClkzzI9pQgorBtY1gOTPId7xOcdIJbU7GsiMS14qIGxyHfidWHXeZ03u55wAlAVVxOCXmOkPgjY6RS6iEx_DeH4usNNXwEMtLFlxUABa0EIZM7oBfroGgI0Xparj8foCzAs4q9EBEZpctIFED-daWonE4z_HnCAXKIk-FvTEP3lz4IBR-yybBuvdoZ73pDdpGF-Q56MZLeQDow4v7f8PRTtwhEPcg3Khr54Ppc73t2iuWa3wGcefTEG4fyqMhXo0y8K7Yo6o-ZubICofVBgE6pFjLsD2J4x7eMqCJchA4HatDDZMme79RhK1oNp47-Q-7D3pWCrre7tI4f4JWdCt-HlyrAHPKpGHDM6bg5F_C51jrFEOlRSdwO-=w549-h424-no)

 - Click Next -> Create data logs -> Performance counter -> Next

![Create performance counter](https://lh3.googleusercontent.com/mJX1HdQqxAWIFixQJBnkkPZOvOWGzDQ6g4MnCiLVkMg9GuB2ZMVBdpOEiSZT6HkPzGor0bEC9Og1GrIoGteVdWOmXTPAL1YHP51PEWXYb4QN5TmlUUzaHECvvXBTFnDHGn46nFZ56MaG91nE7Wxipc9YwOda9oETXav26jQtSFS6WhJBeeer9zdt3jG_BqMl2hHApZSISrt5yMh6IOThnyrCEvnQyPZu_VCk4zXOy4NEQFeS53RTim1b5_IRMeTyi1V2_rN2gxqzqGMbR75Urf0DMYPAMWrt3nXsUG4K0UhfG1w0A6ImUW_9RP1hTiue7eC2zZpQPkUdAi83aejVKr7iJI7ojxMjroDcUm_jmOdEnkk6pb2KjERk_2-clC_GVciJZSqiUnfq37gBcTTTcMyGCQYG6p1utNA-PVNid7BGudj4zUUXx_05ifvfIMQtY34DKBl_Wr8Ru0WM_LWxttsI9UURlRTSYaDwVFgAkYk73xAU-MhwuoyD2tDpP1nkrAj2iaCEiUwnRSXoKscoZhuBrSys2faKWhI4hRJ5Oz1kG-lBdfEV4XlkUROPKbXJ0KrbjqAJ5YW9Xpm9tlGJdOyqxvTnwRz3q5tcfS3ywaCtD-u2cl4U=w549-h424-no)

 - Click Add in the next screen

![Add performance counter](https://lh3.googleusercontent.com/JFLlop1dJZnneQeyMfT6Bqv4L24h5zO3owzYB7ye5PaozIRO5L-A7XQSO3q7o3HSxc8hasKXbft2rfWPQxvyaJvkcQUfaYbLw022PHbgM9i4TGzhhDrxB4aMv_Af9CKwwmX2ILsEWYOZv3OtdMSbXKbfgjogCMElxQk7CpQ2CwJdxj9VaE5MC7FoW98O-DhsXBmoFMwNIfcHGTciF__IjFs2VNa6lrMcRH95k5wtTtW5FDmHLsYqHxYZvqN-XKyGRJ0YPGKDwh7aXxlRohx3kvW-PoFvfCKfThxCKtCm52f3Kd-Gay5juvBsNqUiSelz_MA6CXdoyyJrJDcr6_9IUyoJrGNDOF0cBo-A_J0NOlNqPIV_g0zFrzaTQ075Ocz9c5mLLziUCOmjbBvM03dRAcG_FT2w4KB3MFFdHk28p7-_T41BaplCACr7Q3VMJy8PBor1xKj47OvoL62pOvRFRCa4A_R4dCYpFR6ijygHPFoGV21A2S2AzqovFUvUjPvot7nZND5yEVM2yjkVARJZ35icYxO70A8MjU37lJsJvHsGBYDyYoQlv8_ObgJfMGHm8j0RV1pZNWIs2em4lyp26i30YfbEFXGffPaMfYcx4IStXDtjE_jx=w549-h424-no)

 - Add Available Bytes, Available MBytes, Page faults per second, Pages per second under Memory
 - Add % disk time, Average disk second per read, Average disk second per write, Current disk queue length, disk bytes per second, disk transfer per second under Physical Disk
 - % privileged Time, % processor time under Processor
 - Add Freespace scans per second, Fullscan/sec  under SQL Server access methods
 - Add buffer cache hit ratio, checkpoint pages/sec, free pages, lazy writes/sec, page life expectancy under SQL Server buffer manager
 - Add user conections under SQL Server general statistics
 - Add Total latch wait time under SQL Server latches
 - Add Lock timeouts/sec, Lock wait time, number of deadlocks/sec under SQL Server locks
 - Under SQL Server memory manager, add memory grants pending, targe server memory and total server memory
 - Under SQL Server SQL statistics, add batch requests/sec, SQL compilations/sec, SQL re-compilations/sec
 - Under System, add context switches/sec, processor queue length
 - Click OK -> Next -> Next -> Finish
 - Right click this new collector set under User defined and choose start

When one needs to see the report, stop this collector and open the collector file and view as report.

[Source](https://www.youtube.com/watch?v=E7QIoHj1FeI)
