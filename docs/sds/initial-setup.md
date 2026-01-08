# Initial Setup

## Requirements

The sample framework data uses the steelwork catalog, spec, and property data from the databases in the AVEVA **ACP** project. To use the sample framework, include the following databases in your project:

| Name                     | DB No. | Description                                            |
| ------------------------ | -----: | ------------------------------------------------------ |
| MASTER/STL_PROFILE_CATA  | 250700 | AVEVA Master Steelwork Profile Catalogue database      |
| MASTER/STL_PROFILE_SPECS | 250701 | AVEVA Master Steelwork Profile Specifications database |
| MASTER/STL_PROP          | 251709 | AVEVA E3D Structural Design Property database          |

## Prepare Sample Catalog

To prepare the sample catalog for your project, follow these steps:

1. Open the **Paragon** module.

2. Set the CE to a top-level element so that the sample CATA and SPWL will be created immediately after it.

   ![Set CE](_images/setup_set_ce_to_cata.png)

3. On the **SDS** tab, click **Load Master**.

   ![Load Master](_images/setup_menu_load_master.png)

4. In the confirmation dialog, click **Yes**.

   ![Confirm](_images/setup_confirm.png)

5. Make sure that `/SDS-CATA` and `/SDS-SPWL` have been created.

   ![New Elements](_images/setup_new_cata_spec.png)

## Prepare Drawing Template Library

To prepare the sample drawing template library for your project, follow these steps:

1. Open the **Draw** module.

2. Set the CE to a top-level element so that the sample DEPT and STYLWL will be created immediately after it.

   ![Set CE](_images/setup_set_ce_to_dept.png)

3. On the **SDS** tab, click **Load Master**.

   ![Load Master](_images/setup_menu_load_master.png)

4. In the confirmation dialog, click **Yes**.

   ![Confirm](_images/setup_confirm.png)

5. Make sure that `/FES-LIBRARIES` and `/FES-PENSTYLES` have been created.

   ![New Elements](_images/setup_new_dept_stylwl.png)
