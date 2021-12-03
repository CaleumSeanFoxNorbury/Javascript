# Generic Tab Renderer

Mithil Components for generically rendering clickable tabs, with types and schemas to match exspectations.

## Interfaces 

### Tabs

```
export interface Tabs {
  label: string;
  // f7-icon object includes two strings
  // the f7-object is used if present
  icon?: Tab;
  // if the tab is a title
  title?: boolean;
}
```

### Tab

```
export interface Tab {
  // name of the f7-icon
  label: string;
  // colour of the background, in hex or css short
  colour?: string;
}

```

## Components 

### navbar.ts

```
// import style

// import interfaces or classes

let selectedTab: string = 'Home';

export default function TabRenderer(): m.Component {
  const res: m.Component = {
    view() {
      let tabs: Tab[] = [
        {label: 'NavBar', title: true},
        {label: 'Home ', icon: {label: 'house', colour: 'lightgreen'}},
        {label: 'Contact', icon: {label: 'map', colour: '#fb654e'}},
        {label: 'Pages', title: true},
        {label: 'Page One', icon: {label: '', colour: ''}},
        {label: 'Page Two', icon: {label: '', colour: ''}}
      ];

      return
          m('.row', {style: {height: '100%'}},
            m('.leftpanel',
              m('.top.left.m4', m(BackButton, {destination: '/dashboard'})),
              m('div', {style: {height: '18px'}}), m('.subheading', 'Settings'),
              m('div', {style: {height: '30px'}}),
              tabs.map(
                  tab => m(Tab, {
                    tab: tab,
                    selected: selectedTab,
                    onTabChange:
                        (tab: string) => { selectedTab = tab; }
                  }))));
    }
  };

  return res;
}
```

### tab.ts

```
// import style

// import interfaces or classes

export interface Attrs {
  tab: Tabs;
  selected?: string;
  onTabChange: (x: string) => void;
}

const Tab: m.Component<Attrs> = {
  view({attrs: {tab, selected, onTabChange}}) {
    if (tab.title) {
      return m('.subheading', tab.label);
    } else {
      return m(
          '.row.aicenter.jcspace-between', {
            onclick: () => { onTabChange(tab.label); },
            style: {
              borderTop: '1px solid #a4a8a8',
              borderBottom: '1px solid #a4a8a8'
            },
            className: (tab.label === selected) ? 'selected selectedcol' : ''
          },
          m('.round.m2', {style: {backgroundColor: tab.icon?.colour}},
            m('i.f7-icons', tab.icon?.label)),
          m('.bold', tab.label),
          m('i.f7-icons', {className: (tab.label === selected) ? 'selectedcol' : ''}, 'chevron_compact_right'));
    }
  }
};

export default Tab;

```

# Styles 

```
  TODO
```
