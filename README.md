# catproduct_bootstrap

## CatClickerApp Requirements

1.	Data Entity: Cat <br>
a.	Fields: CatName, CatClicks, CatAge, CatImage and CatNickNames <br>
2.	Data List: A file with an array of some Cats for initialization. These Cats will need to get stored in Local Storage if there are no Cats or no Cat variable is defined in Local Storage<br>
a.	After Initialization all data is fetched from Local Storage<br>
3.	UI<br>
a.	4 panels <br>
i.	Left Nav with Cat Name and a Chip to show the number of times the cat got clicked <br>
ii.	Center: Cat Card with name, image, nick names and age <br>
iii.	Right: Form to Update the Cat with fields Cat Name, Cat Image and Cat Clicks (Optional)
iv.	Bottom across full width: Cat Image Gallery <br>
4.	Events <br>
a.	Left Nav when a Cat is clicked that Cat need to be shown in the center and the selected Cat list item background color needs to be changed <br>
b.	When a user clicks a Cat Image in center panel, the number of clicks need to be incremented by 1<br>
c.	When a user clicks a Cat Image in the bottom panel gallery, the number of clicks need to be incremented by 1 and the center panel should show the clicked Cat and the focus to move to the center panel <br>
d.	Whenever the click count increases, update the age based on the number of clicks<br>
i.	0 to 5: Infant<br>
ii.	6 to 12: Child<br>
iii.	13 to 25: Young<br>
iv.	26 to 40: Middle-Age<br>
v.	41 to 60: Old<br>
vi.	>61: Very Old<br>
e.	Create New Cat or Update Existing Cat (Optional)<br>
i.	Right nav will need to have a button to open Edit form<br>
ii.	When the form is opened the fields will have default values of the active Cat (the Cat that is clicked and shown in the center) need<br>
iii.	User can change the Image or the click count for an existing Cat<br>
iv.	User can change the name - is like adding a new Cat with the given image and the click count as values<br>
v.	User can save and the saved cat will become active - example, a new cat is added, that Cat is selected in the list  and also shown in the center panel<br>
vi.	When the User updates, the values get updated and that Cat becomes active<br>
vii.	When the user Saves, the above will happen and the form gets closed<br>
viii.	User can also Cancel without any changes and the form gets closed<br>
5.	Development<br>
a.	React<br>
b.	Gulp<br>
c.	Bootstrap 4 components<br>
d.	Responsive<br>
e.	All UI components need to accept values as Props - either field values or call back functions<br>
f.	Manage state at only 1 central place (the highest level App component)<br>
g.	Example <br>
i.	CatDetail UI Component will take properties as a Cat Object with its fields and it also takes a property of Click function<br>
ii.	When a Cat gets clicked this Callback function is provided to its parent Component<br>
iii.	Parent Component updates the Local Storage and it also updates the State (Active Cat)<br>
iv.	When the state is updated all the child components will get re-rendered automatically<br>
v.	Basically above is the key programming practice of a UI component accepting props for fields and call back functions (events) and not storing any state<br>
h.	For Reference UI Components <br>
i.	App (highest level parent component that contains the following UI components) <br>
ii.	CatList<br>
iii.	CatListItem<br>
iv.	CatDetail<br>
v.	CatForm (Optional)<br>
vi.	CatGallery<br>
vii.	CatGalleryItem<br>



> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).
