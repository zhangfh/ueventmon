kernel :
+    char *buf;
+    char *envp[3];
     FUNC_ENTRY();
+    buf = kmalloc(32,GFP_ATOMIC);
+    if(!buf){
+               printk("%s kmalloc failed\n", __func__);
+               return;
+    }
+    envp[0] = "name=ble";
+    snprintf(buf , 32 , "status=%d",1);//test
+    envp[1] = buf;
+    envp[2] = NULL;

+       kobject_uevent_env(&misc.this_device->kobj,KOBJ_CHANGE,envp);
     }
+    kfree(buf);


change@/devices/virtual/misc/vble
  ACTION=change
  DEVPATH=/devices/virtual/misc/vble
  SUBSYSTEM=misc
  name=ble
  status=1
  MAJOR=10
  MINOR=60
  DEVNAME=vble
  SEQNUM=837
