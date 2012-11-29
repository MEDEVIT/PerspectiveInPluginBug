BUG
===

This example project demonstrates following bug:

 * If at application-startup the selected perspective is in another plugin it will crash

Steps to reproduce
==================

 * Create new RCP-Application with a Application.e4xmi
 * Create new PlugIn with a model-fragment
 * Define a perspective in the model-fragment and contribute it to the perspective-stack
 * Add the plugin to the product
 * Implement a little perspective switcher to switch between perspectives in Application.e4xmi and fragment.e4xmi
 * Restart the application

Working
-------

When the selected perspective is in Application.e4xmi it will restart without errors.

Broken
------

When the selected perspective is in fragment.e4xmi it will throw an exception:

    java.lang.NullPointerException
      at org.eclipse.e4.ui.model.internal.ModelUtils.getContainingContext(ModelUtils.java:181)
      at org.eclipse.e4.ui.internal.workbench.ModelServiceImpl.getContainingContext(ModelServiceImpl.java:276)
      at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine.getContext(PartRenderingEngine.java:675)
      at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine.safeCreateGui(PartRenderingEngine.java:728)
      at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine.access$2(PartRenderingEngine.java:703)
      at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine$7.run(PartRenderingEngine.java:697)
      at org.eclipse.core.runtime.SafeRunner.run(SafeRunner.java:42)
        (...)

