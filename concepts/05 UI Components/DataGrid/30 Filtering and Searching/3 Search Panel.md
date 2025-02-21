The search panel allows a user to search for values in several columns at once. Search is case-insensitive.

![DevExtreme HTML5 JavaScript jQuery Angular Knockout UI component DataGrid SearchPanel](/images/DataGrid/visual_elements/search_panel.png)

To make the search panel visible, assign **true** to the [searchPanel](/api-reference/10%20UI%20Components/GridBase/1%20Configuration/searchPanel '/Documentation/ApiReference/UI_Components/dxDataGrid/Configuration/searchPanel/').**visible** property. You can set a column's [allowSearch](/api-reference/_hidden/GridBaseColumn/allowSearch.md '/Documentation/ApiReference/UI_Components/dxDataGrid/Configuration/columns/#allowSearch') property to **false** if it should be excluded from searching. Note that this property inherits the [allowFiltering](/api-reference/_hidden/dxDataGridColumn/allowFiltering.md '/Documentation/ApiReference/UI_Components/dxDataGrid/Configuration/columns/#allowFiltering') property's value by default.

---
##### jQuery

    <!--JavaScript-->$(function() {
        $("#dataGridContainer").dxDataGrid({
            // ...
            searchPanel: { visible: true },
            columns: [{
                // ...
                allowSearch: false
            }]
        });
    });

##### Angular
    
    <!--HTML-->
    <dx-data-grid ... >
        <dxo-search-panel [visible]="true"></dxo-search-panel>
        <dxi-column [allowSearch]="false" ... ></dxi-column>
    </dx-data-grid>

    <!--TypeScript-->
    import { DxDataGridModule } from "devextreme-angular";
    // ...
    export class AppComponent {
        // ...
    }
    @NgModule({
        imports: [
            // ...
            DxDataGridModule
        ],
        // ...
    })

##### Vue

    <!-- tab: App.vue -->
    <template>
        <DxDataGrid ... >
           <DxSearchPanel :visible="true" />
           <DxColumn :allow-search="false" />
        </DxDataGrid>
    </template>

    <script>
    import 'devextreme/dist/css/dx.light.css';

    import DxDataGrid, {
        DxColumn,
        DxSearchPanel
    } from 'devextreme-vue/data-grid';

    export default {
        components: {
            DxDataGrid,
            DxColumn,
            DxSearchPanel
        }
    }
    </script>

##### React

    <!-- tab: App.js -->
    import React from 'react';
    import 'devextreme/dist/css/dx.light.css';

    import DataGrid, {
        Column,
        SearchPanel
    } from 'devextreme-react/data-grid';

    function App() {
        return (
            <DataGrid ... >
                <SearchPanel visible={true} />
                <Column allowSearch={false} />
            </DataGrid>
        );
    }

    export default App;

##### ASP.NET MVC Controls

    <!--Razor C#-->
    @(Html.DevExtreme().DataGrid()
        @* ... *@
        .SearchPanel(sp => sp.Visible(true))
        .Columns(columns => {
            columns.Add().AllowSearch(false);
        })
    )    

---


Use the **searchPanel**.[text](/api-reference/10%20UI%20Components/GridBase/1%20Configuration/searchPanel/text.md '/Documentation/ApiReference/UI_Components/dxDataGrid/Configuration/searchPanel/#text') property to predefine the search value. You can also change it at runtime by calling the [searchByText(text)](/api-reference/10%20UI%20Components/GridBase/3%20Methods/searchByText(text).md '/Documentation/ApiReference/UI_Components/dxDataGrid/Methods/#searchByTexttext') method:

---
##### jQuery

    <!--JavaScript-->
    $(function() {
        $("#dataGridContainer").dxDataGrid({
            // ...
            searchPanel: {
                visible: true,
                text: "4/1/2015"
            }
        });
    });

<!---->

    <!--JavaScript-->
    $("#dataGridContainer").dxDataGrid("instance").searchByText("1/29/2016");

##### Angular

    <!--HTML-->
    <dx-data-grid ... >
        <dxo-search-panel 
            [visible]="true" 
            [(text)]="searchText">
        </dxo-search-panel>
    </dx-data-grid>

    <!--TypeScript-->
    import { DxDataGridModule } from "devextreme-angular";
    // ...
    export class AppComponent {
        searchText: string = "4/1/2015";
        setSearchValue (searchText) {
            this.searchText = searchText;
        }
    }
    @NgModule({
        imports: [
            // ...
            DxDataGridModule
        ],
        // ...
    })

##### Vue

    <!-- tab: App.vue -->
    <template>
        <DxDataGrid ... >
            <DxSearchPanel 
                :visible="true"
                v-model:text="searchText" 
            />
        </DxDataGrid>
    </template>

    <script>
    import 'devextreme/dist/css/dx.light.css';

    import DxDataGrid, {
        DxSearchPanel
    } from 'devextreme-vue/data-grid';

    export default {
        components: {
            DxDataGrid,
            DxSearchPanel
        },
        data() {
           return {
               searchText: "4/1/2015",
           }
        },
        methods: {
            setSearchValue (searchText) {
                this.searchText = searchText;
            }
        }
    }
    </script>

##### React

    <!-- tab: App.js -->
    import React, { useState, useCallback } from 'react';
    import 'devextreme/dist/css/dx.light.css';

    import DataGrid, {
        SearchPanel
    } from 'devextreme-react/data-grid';

    function App() {
        const [searchText, setSearchText] = useState("4/1/2015");

        const onOptionChanged = useCallback((e) => {
            if (e.fullName === "searchPanel.text") {
                setSearchText(e.value);
            }
        }, []);

        return (
            <DataGrid onOptionChanged={onOptionChanged} ... >
                <SearchPanel 
                    visible={true}
                    text={searchText} 
                />
            </DataGrid>
        );
    }

    export default App;


##### ASP.NET MVC Controls

    <!--Razor C#-->
    @(Html.DevExtreme().DataGrid()
        @* ... *@
        .ID("dataGridContainer")
        .SearchPanel(sp => sp
            .Visible(true)
            .Text("4/1/2015")
        )
    )  

    <script type="text/javascript">
        $("#dataGridContainer").dxDataGrid("instance").searchByText("1/29/2016");
    </script>

---

Searching is performed differently depending on a column's [data type](/api-reference/_hidden/GridBaseColumn/dataType.md '/Documentation/ApiReference/UI_Components/dxDataGrid/Configuration/columns/#dataType'). Numeric, Boolean, and date columns require that a user enters a full value into the search panel. Searching columns containing string values and specifying the search value using the API requires entering only a part of a value.

#####See Also#####
- [Filtering API - Initial and Runtime Filtering](/concepts/05%20UI%20Components/DataGrid/30%20Filtering%20and%20Searching/6%20API/1%20Initial%20and%20Runtime%20Filtering.md '/Documentation/Guide/UI_Components/DataGrid/Filtering_and_Searching/#API/Initial_and_Runtime_Filtering')
- [remoteOperations](/api-reference/10%20UI%20Components/dxDataGrid/1%20Configuration/remoteOperations '/Documentation/ApiReference/UI_Components/dxDataGrid/Configuration/remoteOperations/')
- [DataGrid Demos](https://js.devexpress.com/Demos/WidgetsGallery/Demo/DataGrid/Filtering)
