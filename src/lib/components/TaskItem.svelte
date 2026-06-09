<script>

let {
	item,
	toggleTask,
	deleteTask,
	editTask
}
=
$props();

let editing =
$state(false);

let editedText =
$state("");

function startEdit() {

	editing =
	true;

	editedText =
	item.text;

}

function saveEdit() {

	if (
	editedText
	.trim()
	) {

	editTask(
	item.id,
	editedText
	);

	}

	editing =
	false;

}

</script>

<li
class:completed=
{item.completed}
>

<div class="left">

<input
type="checkbox"

checked=
{item.completed}

onchange={()=>

toggleTask(
item.id
)

}
/>

{#if editing}

<input

class="edit-input"

bind:value=
{editedText}

onkeydown=
{(e)=>

e.key
===
"Enter"

&&

saveEdit()

}

/>

{:else}

<span
class="task-text"

class:done=
{item.completed}
>

{item.text}

</span>

{/if}

</div>

<div class="actions">

{#if editing}

<button
class="save"

onclick=
{saveEdit}
>

Save

</button>

{:else}

<button
class="edit"

onclick=
{startEdit}
>

Edit

</button>

{/if}

<button

class="delete"

onclick={()=>

deleteTask(
item.id
)

}

>

Delete

</button>

</div>

</li>

<style>

li{

display:flex;

justify-content:
space-between;

align-items:
center;

padding:
18px;

margin-bottom:
14px;

background:
white;
border-radius:
16px;

box-shadow:

0 8px 20px

rgba(
0,
0,
0,
0.06
);

transition:
0.25s;

}

li:hover{

transform:
translateY(
-2px
);

}



.left{

display:flex;

align-items:
center;

gap:
14px;

flex:
1;

}

.task-text{

font-size:
16px;

font-weight:
500;

word-break:
break-word;

}

.done{

text-decoration:
line-through;

color:
#16a34a;

opacity:
0.7;

}

.actions{

display:flex;

gap:
10px;

}

.edit-input{

width:
100%;

padding:
10px;

border-radius:
10px;

border:
1px solid #ddd;

font-size:
16px;

}

button{

padding:
10px 14px;

border:
none;

border-radius:
10px;

cursor:
pointer;

font-size:
14px;

transition:
0.2s;

}

button:hover{

opacity:
0.9;

}

.edit{

background:
#2563eb;

color:
white;

}

.save{

background:
#16a34a;

color:
white;

}

.delete{

background:
#ef4444;

color:
white;

}

</style>