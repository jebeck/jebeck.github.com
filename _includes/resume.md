<details open>
  <summary>Table of Contents</summary>
  <ul>
    <li><a href="#technical-skills">technical skills</a></li>
    <li><a href="#noteworthy-projects">noteworthy projects</a></li>
    <li><a href="#employment-history">employment history</a></li>
    <li><a href="#education">education</a></li>
  </ul>
</details>

<span class="mission">Front-end focused web application & data visualization engineer. Test-driven, CI approved.</span>

## technical skills

### 😎 highest proficiency

<span class="skills-explainer">The vast majority of my work and side project time employs these skills.</span>

JavaScript:

- single-page apps with the latest tools & frameworks ([React](https://facebook.github.io/react/ 'React'), [React Router](https://github.com/reactjs/react-router#readme 'GitHub: React Router README'), [Redux](http://redux.js.org/ 'redux'))
- interactive data visualization with [D3](https://d3js.org/ 'D3: Data-Driven Documents') and/or React, rendering in SVG
- UI and data visualization animation with CSS3, D3 transitions, various React animation libraries, and/or [GreenSock](https://greensock.com/ 'GreenSock')
- unit testing ([Jest](https://facebook.github.io/jest/ 'Jest: Painless JavaScript testing') or [Mocha](https://mochajs.org/ 'Mocha JavaScript test framework') + [Chai](http://chaijs.com/ 'Chai assertion library'); set up with [Karma](https://karma-runner.github.io/1.0/index.html 'Karma test runner') and either [Travis CI](https://travis-ci.org/ 'Travis CI') or [Circle CI](https://circleci.com/ 'CircleCI'))
- real-time apps on a BaaS (e.g., [Firebase](https://firebase.google.com/ 'Firebase'))
- interactive Node.js CLI tools using [Inquirer.js](https://github.com/SBoudrias/Inquirer.js/#inquirerjs 'Inquirer.js')

HTML5 & CSS3:

- compliance with web standards and WCAG 2.0 for accessibility
- experience with major CSS preprocessors ([Less](http://lesscss.org/ 'Less CSS'), [Sass](http://sass-lang.com/ 'Sass: CSS with superpowers'), [PostCSS](http://postcss.org/ 'PostCSS'))
- modularity and componentization with [CSS modules](https://github.com/css-modules/css-modules#readme 'GitHub: CSS modules README'), [styled components 💅](https://github.com/styled-components/styled-components 'GitHub: styled-components 💅'), or [emotion](https://emotion.sh/ 'emotion CSS-in-JS')

other:

- version control with [git](https://git-scm.com/ 'git') & [GitHub](https://github.com/ 'GitHub')
- managing internal and external dependencies with [npm](https://www.npmjs.com/ 'npm')
- building project pages & documentation on [GitHub Pages](https://pages.github.com/ 'GitHub Pages') with [jekyll](https://jekyllrb.com/ 'jekyll') and/or [GitBook](https://github.com/GitbookIO/gitbook#readme 'GitHub: GitBook README')
- [Markdown](https://daringfireball.net/projects/markdown/ 'Markdown')

### 🙃 other areas of experience

<span class="skills-explainer">Skills I practice only occasionally or practiced in the past.</span>

JavaScript:

- server-rendered React apps with [Next.js](https://github.com/zeit/next.js/ 'GitHub: Next.js')
- Canvas-rendered interactive data visualization with D3 and/or React
- WebGL-rendered interactive data visualization with D3 and/or React via [three.js](https://threejs.org/ 'three.js')
- end-to-end testing with [Nightwatch.js](http://nightwatchjs.org/ 'Nightwatch.js')
- static typing in JavaScript with [flow](https://flowtype.org/ 'flow: a static type checker for JavaScript')

Python:

- scientific computing with [SciPy](https://www.scipy.org/ 'SciPy'), [pandas](http://pandas.pydata.org/ 'pandas: Python data analysis library'), &c
- natural language processing with [NLTK](http://www.nltk.org/ 'Python natural language toolkit')

[R](https://www.r-project.org/ 'The R project for statistical computing'):

- statistical data analysis
- data visualization with [ggplot2](http://ggplot2.org/ 'ggplot2')

### 🤔 (as of yet undeveloped) interests

<span class="skills-explainer">Things on my never-ending TODO list!</span>

- native iOS and Android application development with [React Native](https://facebook.github.io/react-native/ 'React Native')
- native iOS application development with [Swift](https://developer.apple.com/swift/ 'Swift programming language')
- learn a functional language (most likely [elm](http://elm-lang.org/ 'elm: the best of functional programming in your browser') or [Clojure](https://clojure.org/ 'Clojure') and/or [ClojureScript](http://clojure.org/about/clojurescript 'ClojureScript'))
- learn to use [ReactiveX](http://reactivex.io/ 'ReactiveX'), most likely [RxJS](https://github.com/ReactiveX/rxjs 'GitHub: RxJS')

## noteworthy projects

### ⚛️ AA React at Stitch Fix

Designed and led development of a library of React components for internal use within Stitch Fix’s [Algorithms & Analytics department (“AA”)](https://multithreaded.stitchfix.com/algorithms/ 'Stitch Fix Algorithms'). The components handle data fetching and storage from and to AA’s shared data warehouse and other internal services.

### 👩‍🎤 rappstar and other CLI tools at Stitch Fix

Designed and led development of a wizard-style CLI wrapper around [create-react-app (CRA)](https://facebook.github.io/create-react-app/ 'Create React App') to facilitate quick and beginner-friendly app development by data scientists. The tool customizes the output of CRA to include internal dependencies and configuration. Other CLI tools include a script for building a CRA app and pushing the result to an S3 bucket set up for static web hosting.

### 📊 Data Visualization at Tidepool

Led initial development of Tidepool's data visualization libraries [tideline](https://github.com/tidepool-org/tideline 'GitHub: tideline') and [@tidepool/viz](https://github.com/tidepool-org/viz 'GitHub: @tidepool/viz'). Both libraries employ React and D3 to implement UI components for interactive data visualizations in Tidepool's main web application [blip](https://github.com/tidepool-org/blip 'GitHub: blip') as well as utilities for data (pre-)processing and on-the-fly calculation of a variety of statistical measures.

### 🚀 Redux Migrations at Tidepool

Led the migration of Tidepool's [uploader](https://github.com/tidepool-org/chrome-uploader 'GitHub: chrome-uploader') (a Chrome app) and [blip](https://github.com/tidepool-org/blip 'GitHub: blip') (a web application) to use [Redux](http://redux.js.org/ 'Redux') for state management, vastly increasing test coverage for both applications in the process.

### 🕰 "Bootstrapping" to UTC at Tidepool

Designed and implemented (in the Tidepool [uploader](https://github.com/tidepool-org/chrome-uploader 'GitHub: chrome-uploader')) an algorithm—dubbed "bootstrapping to UTC"—for inferring the UTC timestamp from device-relative display timestamps on diabetes devices. For more information, refer to [the technical documentation](http://developer.tidepool.io/chrome-uploader/docs/BootstrappingToUTC.html 'BtUTC technical documentation') or [the less technical blog post](http://tidepool.org/all/its-a-matter-of-time/ 'Tidepool Blog: It's a Matter of Time') explaining the feature.

### 🚎 Apps for Philly Transit Hackathon

Member of the winning team at the [2013 Apps for Philly Transit Hackathon](http://technical.ly/philly/2013/10/02/apps-philly-transit-hackathon-winners/ 'Technically Philly: 2013 Apps for Philly Transit Hackathon Winners'). Our project ['PHL+ to Work'](http://janabeck.com/PHLWork/ 'PHL+ to Work') ([code on GitHub](https://github.com/jebeck/PHLWork 'GitHub: PHLWork')) provides a visual interface (built with D3 and [Leaflet](http://leafletjs.com/ 'Leaflet')) for searching American Community Survey data connecting locations (specifically census tracts) where residents of the greater Philadelphia area live to the locations where those residents commute to work.

### 🌳 Annotald at the University of Pennsylvania

Contributed to [Annotald](http://annotald.github.io/ 'Annotald'), a WebKit browser-based GUI annotation tool for constructing large corpora of syntactically annotated sentences in the Penn [Treebank](https://en.wikipedia.org/wiki/Treebank 'Wikipedia: Treebank') format used by researchers in the University of Pennsylvania's linguistics department as well as at the University of Iceland, Newcastle University, and the University of York. My contributions included a refactoring of the CSS to allow users to define a customized color theme as well as helping to design and implement the [limited display mode](http://annotald.github.io/user.html#limiteddisplay 'Annotald User Manual: limited display mode').

## employment history

| 2017–present | Data Visualization Engineer, Stitch Fix Algorithms
| | San Francisco, CA |
| 2013–2017 | Software Engineer, Tidepool Project
| | San Francisco, CA |
| 2010–2011 | Teaching Assistant, Linguistics Department, University of Pennsylvania |
| | Philadelphia, PA |
| 2008 | Development Assistant, Foundation for Individual Rights in Education |
| | Philadelphia, PA |
| 2007–2008 | Collection Development Assistant, Van Pelt Library, University of Pennsylvania |
| | Philadelphia, PA |
| 2006 | E-Tutor, Computer Science Department, New York University |
| | New York, NY |
| 2005–2007 | Sales Associate, The Scholastic Store |
| | New York, NY |
| 2004–2005 | Book Review Intern, Library Journal |
| | New York, NY |

## education

- M.A. in Linguistics. School of Arts & Sciences, University of Pennsylvania, 2013.
- B.A. in Individualized Study, _summa cum laude_. Gallatin School, New York University, 2007.
