<div align="center">

<h1>
<a href="https://shipixen.com" target="_blank">
  <img height="120px" src="https://user-images.githubusercontent.com/1515742/281076422-8c4a9926-2885-4786-a69a-d79ab0c8dc5c.png" alt="Shipixen Logo" />
</a>
</h1>

</div>

Shipixen an app to generate customized boilerplates for your product. Or any website. We generate it & deploy it - then you get the code.

[shipixen.com](https://shipixen.com)

<a href="https://shipixen.com" target="_blank">
  <img src="https://user-images.githubusercontent.com/1515742/281077548-57b24773-3c2a-4e89-b088-cc3945d7037b.png" alt="Shipixen Logo" />
</a>

# kbar

kbar is a simple plug-n-play React component to add a fast, portable, and extensible <kbd>command</kbd> + <kbd>k</kbd> (command palette) interface to your site.

![demo](https://user-images.githubusercontent.com/12195101/143491194-1d3ad5d6-24ac-4e6e-8867-65f643ac2d24.gif)

## Background

<kbd>Command</kbd> + <kbd>k</kbd> interfaces are used to create a web experience where any type of action users would be able to do via clicking can be done through a command menu.

With macOS's Spotlight and Linear's <kbd>command</kbd> + <kbd>k</kbd> experience in mind, kbar aims to be a simple
abstraction to add a fast and extensible <kbd>command</kbd> + <kbd>k</kbd> menu to your site.

## Features

- Built in animations and fully customizable components
- Keyboard navigation support; e.g. <kbd>control</kbd> + <kbd>n</kbd> or <kbd>control</kbd> + <kbd>p</kbd> for the navigation wizards
- Keyboard shortcuts support for registering keystrokes to specific actions; e.g. hit <kbd>t</kbd>
  for Twitter, hit <kbd>?</kbd> to immediate bring up documentation search
- Nested actions enable creation of rich navigation experiences; e.g. hit backspace to navigate to
  the previous action
- Performance as a first class priority; tens of thousands of actions? No problem.
- History management; easily add undo and redo to each action
- Built in screen reader support
- A simple data structure which enables anyone to easily build their own custom components

### Usage

Have a fully functioning command menu for your site in minutes. First, install kbar.

```
npm install kbar
```

There is a single provider which you will wrap your app around; you do not have to wrap your
_entire_ app; however, there are no performance implications by doing so.

```tsx
// app.tsx
import { KBarProvider } from "kbar";

function MyApp() {
  return (
    <KBarProvider>
      // ...
    </KBarProvider>
  );
}
```

Let's add a few default actions. Actions are the core of kbar – an action define what to execute
when a user selects it.

```tsx
  const actions = [
    {
      id: "blog",
      name: "Blog",
      shortcut: ["b"],
      keywords: "writing words",
      perform: () => (window.location.pathname = "blog"),
    },
    {
      id: "contact",
      name: "Contact",
      shortcut: ["c"],
      keywords: "email",
      perform: () => (window.location.pathname = "contact"),
    },
  ]

  return (
    <KBarProvider actions={actions}>
      // ...
    </KBarProvider>
  );
}
```

Next, we will pull in the provided UI components from kbar:

```tsx
// app.tsx
import {
  KBarProvider,
  KBarPortal,
  KBarPositioner,
  KBarAnimator,
  KBarSearch,
  useMatches,
  NO_GROUP
} from "kbar";

// ...
  return (
    <KBarProvider actions={actions}>
      <KBarPortal> // Renders the content outside the root node
        <KBarPositioner> // Centers the content
          <KBarAnimator> // Handles the show/hide and height animations
            <KBarSearch /> // Search input
          </KBarAnimator>
        </KBarPositioner>
      </KBarPortal>
      <MyApp />
    </KBarProvider>;
  );
}
```

At this point hitting <kbd>cmd</kbd>+<kbd>k</kbd> (macOS) or <kbd>ctrl</kbd>+<kbd>k</kbd> (Linux/Windows) will animate in a search input and nothing more.

kbar provides a few utilities to render a performant list of search results.

- `useMatches` at its core returns a flattened list of results and group name based on the current
  search query; i.e. `["Section name", Action, Action, "Another section name", Action, Action]`
- `KBarResults` renders a performant virtualized list of these results

Combine the two utilities to create a powerful search interface:

```tsx
import {
  // ...
  KBarResults,
  useMatches,
  NO_GROUP,
} from "kbar";

// ...
// <KBarAnimator>
//   <KBarSearch />
<RenderResults />;
// ...

function RenderResults() {
  const { results } = useMatches();

  return (
    <KBarResults
      items={results}
      onRender={({ item, active }) =>
        typeof item === "string" ? (
          <div>{item}</div>
        ) : (
          <div
            style={{
              background: active ? "#eee" : "transparent",
            }}
          >
            {item.name}
          </div>
        )
      }
    />
  );
}
```

Hit <kbd>cmd</kbd>+<kbd>k</kbd> (macOS) or <kbd>ctrl</kbd>+<kbd>k</kbd> (Linux/Windows) and you should see a primitive command menu. kbar allows you to have full control over all
aspects of your command menu – refer to the <a href="https://kbar.vercel.app/docs">docs</a> to get
an understanding of further capabilities. Looking forward to see what you build.

## Used by

Listed are some of the various usages of kbar in the wild – check them out! Create a PR to add your
site below.

- [Outline](https://www.getoutline.com/)
- [zenorocha.com](https://zenorocha.com/)
- [griko.id](https://griko.id/)
- [lavya.me](https://www.lavya.me/)
- [OlivierAlexander.com](https://olivier-alexander-com-git-master-olivierdijkstra.vercel.app/)
- [dhritigabani.me](https://dhritigabani.me/)
- [jpedromagalhaes](https://jpedromagalhaes.vercel.app/)
- [animo](https://demo.animo.id/)
- [tobyb.xyz](https://www.tobyb.xyz/)
- [higoralves.dev](https://www.higoralves.dev/)
- [coderdiaz.dev](https://coderdiaz.dev/)
- [NextUI](https://nextui.org/)
- [evm.codes](https://www.evm.codes/)
- [filiphalas.com](https://filiphalas.com/)
- [benslv.dev](https://benslv.dev/)
- [vortex](https://hydralite.io/vortex)
- [ladislavprix](https://ladislavprix.cz/)
- [pixiebrix](https://www.pixiebrix.com/)
- [nfaustino.com](https://nfaustino-com.vercel.app/)
- [bradleyyeo.com](https://bradleyyeo-com.vercel.app/)
- [andredevries.dev](https://www.andredevries.dev/)
- [about-ebon](https://about-ebon.vercel.app/)
- [frankrocha.dev](https://www.frankrocha.dev/)
- [cameronbrill.me](https://www.cameronbrill.me/)
- [codaxx.ml](https://codaxx.ml/)
- [jeremytenjo.com](https://jeremytenjo.com/)
- [villivald.com](https://villivald.com/)
- [maxthestranger](https://code.maxthestranger.com/)
- [koripallopaikat](https://koripallopaikat.com/)
- [alexcarpenter.me](https://alexcarpenter.me/)
- [hackbar](https://github.com/Uier/hackbar)
- [web3kbar](https://web3kbar.vercel.app/)
- [burakgur](https://burakgur-com.vercel.app/)
- [ademilter.com](https://ademilter.com/)
- [anasaraid.me](https://anasaraid.me/)
- [daniloleal.co](https://daniloleal.co/)
- [hyperround](https://github.com/heyAyushh/hyperound)
- [Omnivore](https://omnivore.app)
- [tiagohermano.dev](https://tiagohermano.dev/)
- [tryapis.com](https://tryapis.com/)
- [fillout.com](https://fillout.com/)
- [vinniciusgomes.dev](https://vinniciusgomes.dev/)

## Contributing to kbar

Contributions are welcome!

### New features

Please [open a new issue](https://github.com/timc1/kbar/issues) so we can discuss prior to moving
forward.

### Bug fixes

Please [open a new Pull Request](https://github.com/timc1/kbar/pulls) for the given bug fix.

### Nits and spelling mistakes

Please [open a new issue](https://github.com/timc1/kbar/issues) for things like spelling mistakes
and README tweaks – we will group the issues together and tackle them as a group. Please do not
create a PR for it!

-----------------

Save 100s of hours of work by using Page AI to generate a beautiful website. In just minutes!

| | |
| :- | :- |
| <a href="https://pageai.pro" target="_blank"><img height="60px" src="https://pageai.pro/static/images/logo-square.png" alt="Page AI Logo" /></a> <br/> <b>Page AI</b> <br/> AI Website Generator that designs and writes clean code. <br/><br/> Try the app on <a href="https://pageai.pro">pageai.pro</a>. | <a href="https://pageai.pro" target="_blank"><img width="300px" src="https://user-images.githubusercontent.com/1515742/281077548-57b24773-3c2a-4e89-b088-cc3945d7037b.png" alt="Page AI Logo" /></a> |

-----------------

Apihustle is a collection of tools to test, improve and get to know your API inside and out. <br/>
[apihustle.com](https://apihustle.com) <br/>

|                                                                                                                                                                                        |              |                                                          |                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------- | :------------------------------------------------------- | :------------------------------------------- |
| <a href="https://pageai.pro" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/9bfbfe6f-add9-45de-aaf2-5c6043a47e41" alt="Page AI Logo" /></a>        | **Page AI**  | AI Website Generator that designs and writes clean code. | [pageai.pro](https://pageai.pro)             |
| <a href="https://shipixen.com" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/e1deba72-328e-4d3c-9c62-11ab77184561" alt="Shipixen Logo" /></a>     | **Shipixen** | Create a personalized blog & landing page in minutes     | [shipixen.com](https://shipixen.com)         |
| <a href="https://pageui.dev" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/b8815b62-598a-4fca-bc27-c03e66c8b105" alt="Page UI Logo" /></a>        | **Page UI**  | Landing page UI components for React & Next.js           | [pageui.dev](https://pageui.dev)             |
| <a href="https://clobbr.app" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/cb3e64e2-efaa-436b-ae6d-0ea4b47e4004" alt="Clobbr Logo" /></a>         | **Clobbr**   | Load test your API endpoints.                            | [clobbr.app](https://clobbr.app)             |
| <a href="https://crontap.com" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/38a3d734-d1ca-4f92-9cfb-ada52b9f2ffb" alt="Crontap Logo" /></a>       | **Crontap**  | Schedule API calls using cron syntax.                    | [crontap.com](https://crontap.com)           |
| <a href="https://tool.crontap.com" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/545f7618-ff2c-47fa-ad17-e17e38155f55" alt="CronTool Logo" /></a> | **CronTool** | Debug multiple cron expressions on a calendar.           | [tool.crontap.com](https://tool.crontap.com) |

-----------------

<a href="https://apihustle.com" target="_blank">
  <img height="60px" src="https://user-images.githubusercontent.com/1515742/215217833-c07183d2-f688-4d1c-86ea-329f3b28f81c.svg" alt="Apihustle Logo" />
</a>

-----------------

