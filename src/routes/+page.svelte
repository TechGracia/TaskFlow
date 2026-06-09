<script>
import { onMount } from "svelte";
import TaskItem from "$lib/components/TaskItem.svelte";

let task = $state("");
let tasks = $state([]);

let filter = $state("all");

onMount(() => {

	const saved =
	localStorage.getItem(
	"tasks"
	);

	if (saved) {
		tasks =
		JSON.parse(saved);
	}

});

function saveTasks() {

	localStorage.setItem(
	"tasks",
	JSON.stringify(tasks)
	);

}

function addTask() {

	if (!task.trim())
	return;

	tasks.push({

	id:
	Date.now(),

	text:
	task,

	completed:
	false

	});

	saveTasks();

	task = "";

}

function deleteTask(id) {

	tasks =
	tasks.filter(
	t =>
	t.id !== id
	);

	saveTasks();

}

function toggleTask(id) {

	const current =
	tasks.find(
	t =>
	t.id === id
	);

	if (current) {

	current.completed =
	!current.completed;

	saveTasks();

	}

}

function editTask(
id,
newText
) {

	const current =
	tasks.find(
	t =>
	t.id === id
	);

	if (current) {

	current.text =
	newText;

	saveTasks();

	}

}

function clearCompleted() {

	tasks =
	tasks.filter(
	t =>
	!t.completed
	);

	saveTasks();

}

function filteredTasks() {

	if (
	filter ===
	"active"
	) {

	return tasks.filter(
	t =>
	!t.completed
	);

	}

	if (
	filter ===
	"completed"
	) {

	return tasks.filter(
	t =>
	t.completed
	);

	}

	return tasks;

}

function progress() {

	if (
	tasks.length === 0
	)
	return 0;

	return (

	tasks.filter(
	t =>
	t.completed
	).length

	/

	tasks.length

	) * 100;

}
</script>

<div class="container">

<div class="header">

<div>

<h1>
TaskFlow
</h1>

<p class="subtitle">

Stay organized.
Finish faster.

</p>

</div>

</div>

<div class="task-input">

<input

bind:value={task}

placeholder=
"Add your next task..."

onkeydown={(e)=>

e.key==="Enter"

&&

addTask()

}

/>

<button
onclick={addTask}
>

＋

</button>

</div>

<div class="filters">

<button
class:active=
{filter==="all"}

onclick={()=>
filter="all"
}
>

All

</button>

<button
class:active=
{filter==="active"}

onclick={()=>
filter="active"
}
>

Active

</button>

<button
class:active=
{filter==="completed"}

onclick={()=>
filter="completed"
}
>

Completed

</button>

</div>

<div class="stats">

<h3>

Total:
{tasks.length}

</h3>

<button

class="clear-btn"

onclick=
{clearCompleted}

>

Clear

</button>

</div>

<p>

Completed:

{
tasks.filter(
t =>
t.completed
).length
}

|

Remaining:

{
tasks.filter(
t =>
!t.completed
).length
}

</p>

<div class="progress">

<div

class="fill"

style:width=
{`${progress()}%`}

></div>

</div>

{#if
filteredTasks()
.length===0
}

<p class="empty">

No tasks yet

</p>

{:else}

<ul>

{#each
filteredTasks()
as item
}

<TaskItem

{item}

{toggleTask}

{deleteTask}

{editTask}

/>

{/each}

</ul>

{/if}

<footer>

Built with ❤️ using Svelte

</footer>

</div>

<style>

:global(body){

margin:0;

font-family:
Arial;

background:

linear-gradient(
135deg,
#eef2ff,
#f8fafc
);

}

.container{

max-width:
720px;

margin:
60px auto;

padding:
35px;

background:
white;

border-radius:
24px;

box-shadow:

0 15px 40px

rgba(
0,
0,
0,
0.08
);

}

.header{

display:flex;

flex-direction:
column;

align-items:
flex-start;

}

.subtitle{

margin-top:
-8px;

color:
#777;

}

.task-input{

display:flex;

gap:
12px;

margin:
30px 0;

}

.task-input input{

flex:1;

height:
56px;

padding:
0 18px;

border-radius:
14px;

}

.task-input button{

width:
80px;

font-size:
24px;

border-radius:
14px;

background:
#4f46e5;

color:
white;

border:
none;

}

.filters{

display:flex;

gap:
10px;

margin-bottom:
20px;

}

.filters button{

border-radius:
999px;

padding:
12px 22px;

}

.filters button.active{

background:
#4f46e5;

color:
white;

border:
none;

}

.stats{

display:flex;

justify-content:
space-between;

align-items:
center;

margin-top:
30px;

}

.clear-btn{

padding:
10px 18px;

background:
#ef4444;

color:
white;

border:
none;

border-radius:
10px;

font-weight:
600;

}

.progress{

height:
12px;

background:
#ddd;

border-radius:
999px;

overflow:
hidden;

margin:
20px 0;

}

.fill{

height:
100%;

background:

linear-gradient(
90deg,
#6366f1,
#8b5cf6
);

transition:
0.3s;

}

ul{

padding:0;

list-style:none;

}

button{

cursor:pointer;

}

.empty{

padding:
40px;

color:
#777;

}

footer{

text-align:
center;

margin-top:
30px;

color:
#777;

font-size:
14px;

}

</style>