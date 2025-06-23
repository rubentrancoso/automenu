# Automenu

Automenu is a Java library that simplifies the creation of Swing menus from XML files. It allows you to build **menu bars**, **context (popup) menus**, and **toolbars** dynamically, linking the XML definition to ready-to-use Swing objects.

## Key Features

- Automatic generation of `JMenuBar`, `JPopupMenu`, and `JToolBar` using XML descriptions.
- Support for action, option (radio), check box menu items, and separators.
- Code organized in *Model* / *View* / *Control* to ease customization.
- Optional handling via [JXPath](https://commons.apache.org/proper/commons-jxpath/) to locate components using XPath expressions.
- Internationalization through `.properties` files (class `I18N`).

## Project Structure

```
src/main/java/org/digitalmonks/automenu
├── ABarMenu.java        # implementation for JMenuBar
├── APopupMenu.java      # implementation for JPopupMenu
├── AToolBarMenu.java    # implementation for JToolBar
├── control/             # event control classes
├── model/               # model entities and mappings
├── support/             # utilities (DOM, I18N)
└── view/                # Swing view rendering
```

The `pom.xml` defines the Maven artifact `org.digitalmonks:automenu`.

## Usage Example

1. **Define the menu XML** (simple `abarmenu` example):

```xml
<abarmenu>
    <menu font="SansSerif" size="12" icons="true" adjustIcons="true">
        <submenu name="File">
            <item type="action" id="new" name="New" icon="icons/new.png" />
            <item type="action" id="exit" name="Exit" shortcut="S" />
        </submenu>
        <submenu name="Help">
            <item type="action" id="about" name="About" />
        </submenu>
    </menu>
</abarmenu>
```

2. **Load the menu in your Swing application:**

```java
JFrame frame = new JFrame();
Object actionHandler = this; // class implementing AAutoMenuListener
ABarMenu menu = new ABarMenu("menu.xml", frame, actionHandler);
```

3. **Implement the event handling** in the class provided as `actionHandler` by implementing `AAutoMenuListener`.

## Building

This project uses Maven. To generate the JAR run:

```bash
mvn package
```

The resulting artifact will be in `target/automenu-0.0.1-SNAPSHOT.jar`.

## Notes

- The library looks for message files in the `properties/` folder for internationalization.
- To customize the appearance you can define font, size, and icon usage in the menu XML itself.
- If the project is used in modules with restricted network access, you may need to configure local Maven repositories to compile.
