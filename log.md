# Development Log

This is my first TypeScript Dockerised React project.

## [Hello World](https://handsonreact.com/docs/labs/ts/01-CreatingNewProject)

1. ### Create project

In project's directory, use the following command (to use `npm` as the package manager):

`npx create-react-app keeptrack --template typescript --use-npm`

_May need to install the package `create-react-app@5.0.1`_
_This will create a `keeptrack` folder inside the current directory_ 2. ### Run the project

Using `npm start` inside the terminal, ensure the current directory is `keeptrack`.

In the same terminal, stop the project with `Ctrl + C`.

3. ### Make a change, inside `src\App.tsx`

```ts
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.tsx</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          - Learn React + Learn React!!!
        </a>
      </header>
    </div>
  );
}
```

4. ### Styles using CSS

Install `mini.css` using `npm install mini.css@3.0.1`.

To import the `mini.css` into `index.css`, include:

`@import '../node_modules/mini.css/dist/mini-dark.css'`

5. ### Component

Create a component `src/projects/ProjectPage.tsx`, including:

```ts
import React from "react";

function ProjectsPage() {
  return <h1>Projects</h1>;
}

export default ProjectsPage;
```

In `src\App.tsx`, change the content of `App()` to:

```ts
function App() {
  return (
    <div className="container">
      <ProjectsPage />
    </div>
  );
}
```

6. ### Data Modelling

Create a model in `src\projects\models\Project.ts`, used to model a `Project` class:

```ts
export class Project {
  id: number | undefined;
  name: string = "";
  description: string = "";
  imageUrl: string = "";
  contractTypeId: number | undefined;
  contractSignedOn: Date = new Date();
  budget: number = 0;
  isActive: boolean = false;
  get isNew(): boolean {
    return this.id === undefined;
  }

  constructor(initializer?: any) {
    if (!initializer) return;
    if (initializer.id) this.id = initializer.id;
    if (initializer.name) this.name = initializer.name;
    if (initializer.description) this.description = initializer.description;
    if (initializer.imageUrl) this.imageUrl = initializer.imageUrl;
    if (initializer.contractTypeId)
      this.contractTypeId = initializer.contractTypeId;
    if (initializer.contractSignedOn)
      this.contractSignedOn = new Date(initializer.contractSignedOn);
    if (initializer.budget) this.budget = initializer.budget;
    if (initializer.isActive) this.isActive = initializer.isActive;
  }
}
```

Create a mock project data object in `src\projects\MockProjects.ts`:

```ts
import { Project } from "./models/Project";

export const MOCK_PROJECTS = [
  new Project({
    id: 1,
    name: "Johnson - Kutch",
    description:
      "Fully-configurable intermediate framework. Ullam occaecati libero laudantium nihil voluptas omnis.",
    imageUrl: "/assets/placeimg_500_300_arch4.jpg",
    contractTypeId: 3,
    contractSignedOn: "2013-08-04T22:39:41.473Z",
    budget: 54637,
    isActive: false,
  }),
  new Project({
    id: 2,
    name: "Wisozk Group",
    description:
      "Centralized interactive application. Exercitationem nulla ut ipsam vero quasi enim quos doloribus voluptatibus.",
    imageUrl: "/assets/placeimg_500_300_arch1.jpg",
    contractTypeId: 4,
    contractSignedOn: "2012-08-06T21:21:31.419Z",
    budget: 91638,
    isActive: true,
  }),
  new Project({
    id: 3,
    name: "Denesik LLC",
    description:
      "Re-contextualized dynamic moratorium. Aut nulla soluta numquam qui dolor architecto et facere dolores.",
    imageUrl: "/assets/placeimg_500_300_arch12.jpg",
    contractTypeId: 6,
    contractSignedOn: "2016-06-26T18:24:01.706Z",
    budget: 29729,
    isActive: true,
  }),
  new Project({
    id: 4,
    name: "Purdy, Keeling and Smitham",
    description:
      "Innovative 6th generation model. Perferendis libero qui iusto et ullam cum sint molestias vel.",
    imageUrl: "/assets/placeimg_500_300_arch5.jpg",
    contractTypeId: 4,
    contractSignedOn: "2013-05-26T01:10:42.344Z",
    budget: 45660,
    isActive: true,
  }),
  new Project({
    id: 5,
    name: "Kreiger - Waelchi",
    description:
      "Managed logistical migration. Qui quod praesentium accusamus eos hic non error modi et.",
    imageUrl: "/assets/placeimg_500_300_arch12.jpg",
    contractTypeId: 2,
    contractSignedOn: "2009-12-18T21:46:47.944Z",
    budget: 81188,
    isActive: true,
  }),
  new Project({
    id: 6,
    name: "Lesch - Waelchi",
    description:
      "Profound mobile project. Rem consequatur laborum explicabo sint odit et illo voluptas expedita.",
    imageUrl: "/assets/placeimg_500_300_arch1.jpg",
    contractTypeId: 3,
    contractSignedOn: "2016-09-23T21:27:25.035Z",
    budget: 53407,
    isActive: false,
  }),
];
```

7. ### Passing Data to a Component

Create a reusable list component in `src\projects\ProjectList.tsx` that:

- Takes an array of `Project[]` named `projects`
- Displays the `projects` array as a `JSON string`.

```ts
import React from "react";
import { Project } from "./Project";

interface ProjectListProps {
  projects: Project[];
}

function ProjectList({ projects }: ProjectListProps) {
  return <pre>{JSON.stringify(projects, null, " ")}</pre>;
}

export default ProjectList;
```

Pass data into a component property in `src\projects\ProjectsPage.tsx`:

```ts
import React from "react";
import { Project } from "./Project";

interface ProjectListProps {
  projects: Project[];
}

function ProjectList({ projects }: ProjectListProps) {
  return <pre>{JSON.stringify(projects, null, " ")}</pre>;
}

export default ProjectList;
```

8. ### Create another reusable component

Added a `src\projects\ProjectCard.tsx` component.

```ts
import { Project } from './Project';
import React from 'react';

function formatDescription(description: string): string {
  return description.substring(0, 60) + '...';
}

interface ProjectCardProps {
  project: Project;
}

function ProjectCard(props: ProjectCardProps) {
  const { project } = props;
  return (
    <div className="card">
      <img src={project.imageUrl} alt={project.name} />
      <section className="section dark">
        <h5 className="strong">
          <strong>{project.name}</strong>
        </h5>
        <p>{formatDescription(project.description)}</p>
        <p>Budget : {project.budget.toLocaleString()}</p>
      </section>
    </div>
  );
}

export default ProjectCard;
```

Render the reusable component in `src\projects\ProjectList.tsx` (replacing the `<div className="card">` with `<ProjectCard project={project}`>).

9. ### Responding to an Event

Added an edit button in `ProjectCard.tsx`:

```ts
<button className=" bordered">
  <span className="icon-edit "></span>
  Edit
</button>
```

With a handler and event trigger:

```ts
const handleEditClick = (projectBeingEdited: Project) => {
  console.log(projectBeingEdited);
};
return(
  ...
  <button onClick = {() => {handleEditClick(project)}}Edit</button>
)
```