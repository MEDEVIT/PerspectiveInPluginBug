BUG
===

This example project demonstrates following bug:

 * It will crash at application-startup if the selected perspective is in another plugin

Steps to reproduce
==================

 * Create new RCP-Application with a Application.e4xmi
 * Create new PlugIn with a model-fragment (fragment.e4xmi)
 * Define a perspective in the model-fragment and contribute it to the perspective-stack in Application.e4xmi
 * Add the plugin to the product
 * Implement a little perspective-switcher to switch between the perspectives in Application.e4xmi and fragment.e4xmi
 * Restart the application

**Working when** the selected perspective is in Application.e4xmi. It will restart without errors.

**Broken when** the selected perspective is in fragment.e4xmi. It will throw an exception at startup:

    java.lang.NullPointerException
      at org.eclipse.e4.ui.model.internal.ModelUtils.getContainingContext(ModelUtils.java:181)
      at org.eclipse.e4.ui.internal.workbench.ModelServiceImpl.getContainingContext(ModelServiceImpl.java:276)
      at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine.getContext(PartRenderingEngine.java:675)
      at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine.safeCreateGui(PartRenderingEngine.java:728)
      at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine.access$2(PartRenderingEngine.java:703)
      at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine$7.run(PartRenderingEngine.java:697)
      at org.eclipse.core.runtime.SafeRunner.run(SafeRunner.java:42)
        (...)

