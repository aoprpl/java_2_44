# mainFrameController
## 窗口长宽变化监听
如果有什么需要随着窗口变化变化的属性，可以写在这里面。
```java
MainApplication.mainStage.widthProperty().addListener((observable, oldValue, newValue) -> {
            root.setPrefWidth(newValue.doubleValue());
            content.setPrefWidth(newValue.doubleValue()-310);
            for (String key : paneMap.keySet()) {
                Node node = paneMap.get(key);
                changeFitWidth(node);
            }
        });
        MainApplication.mainStage.heightProperty().addListener((observable, oldValue, newValue) -> {
            root.setPrefHeight(newValue.doubleValue());
            separator.setPrefHeight(newValue.doubleValue());
            content.setPrefHeight(newValue.doubleValue());
        });
```
## 菜单按钮
如果想要添加按钮直接找到`adminMenu`等的box下面cv进去，记得改fx:id
```java
<Button fx:id="studentManage" mnemonicParsing="false" prefHeight="67.0" prefWidth="300.0" styleClass="my-Button" stylesheets="@../css/mainframe.css" text="学生管理" textFill="#5c5b5b">
                     <font>
                        <Font size="18.0" />
                     </font>
                  </Button>
```
## 页面切换
```java
studentManage.setOnAction(e -> changeContent("student-panel", "学生管理"));
```
直接在里面写上对应的fxml页面的名字，如果页面是在base文件夹里面的，可以写成`"base/main-frame.fxml"`,`studentManage`就是上面的fx:id
## 内容页面宽度改变
```java
    private void changeFitWidth(Node node) {
        if (node instanceof AnchorPane) {
            ((AnchorPane) node).setPrefWidth(content.getPrefWidth());
        } else if (node instanceof BorderPane) {
            ((BorderPane) node).setPrefWidth(content.getPrefWidth());
        } else if (node instanceof VBox) {
            ((VBox) node).setPrefWidth(content.getPrefWidth());
        } else if (node instanceof HBox) {
            ((HBox) node).setPrefHeight(content.getPrefHeight()); // HBox通常设置高度
            // HBox的高度通常由内容决定，但你可以设置填充、间距等属性
        } else if (node instanceof GridPane) {
            ((GridPane) node).setPrefWidth(content.getPrefWidth());
        } else if (node instanceof StackPane) {
            ((StackPane) node).setPrefWidth(content.getPrefWidth());
        }
    }
```
如果你的切换的页面的根元素在里面没有的话，自己加上就行