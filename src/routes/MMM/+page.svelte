<script>
	import Heading from "$lib/components/Heading.svelte";
	import Dropdown from "$lib/components/Dropdown.svelte";
	import PageHeader from "$lib/components/PageHeader.svelte";
	import PanelBox from "$lib/components/PanelBox.svelte";
    import Section from '$lib/components/Section.svelte';
    import FlexBox from '$lib/components/FlexBox.svelte';
    import Table from "$lib/components/Table.svelte";
    import Link from '$lib/components/Link.svelte';
    import SlideshowNew from "$lib/components/SlideshowNew.svelte";

    let windowWidth;

    const scheduleData = [
        {"Day": "09/22 to 09/26", "Start Time (PT)": "All Day", "Event": "Perilous Proofs"},
        {"Day": "09/26", "Start Time (PT)": "9:00 AM", "Event": "Opening Ceremony <a href='https://us06web.zoom.us/j/88019410306?pwd=l36Mh72xy14BjjhCAJz7xGtXn56FzB.1' target='_blank' style='color:#1B9AAA;'>[Zoom Link]</a>"},
        {"Day": "09/26", "Start Time (PT)": "9:30 AM", "Event": "Solo Stampede <a href='https://bit.ly/MMMdiscord' target='_blank' style='color:#5865F2;'>[Discord]</a>"},
        {"Day": "09/26", "Start Time (PT)": "10:45 AM", "Event": "Lunch"},
        {"Day": "09/26", "Start Time (PT)": "12:00 PM", "Event": "Betting Bonanza <a href='https://bit.ly/MMMdiscord' target='_blank' style='color:#5865F2;'>[Discord]</a>"},
        {"Day": "09/26", "Start Time (PT)": "1:00 PM", "Event": "Meltdown Madness <a href='https://bit.ly/MMMdiscord' target='_blank' style='color:#5865F2;'>[Discord]</a>"},
        {"Day": "09/26", "Start Time (PT)": "2:15 PM", "Event": "Activities (Break out rooms in zoom)"},
        {"Day": "09/26", "Start Time (PT)": "4:30 PM", "Event": "Awards <a href='https://us06web.zoom.us/j/88019410306?pwd=l36Mh72xy14BjjhCAJz7xGtXn56FzB.1' target='_blank' style='color:#1B9AAA;'>[Zoom Link]</a>"},
    ];

    const acceptableData = [
        {"Unacceptable Answers": "61 x 17", "Acceptable Answers": "1037"},
        {"Unacceptable Answers": "Sin (π/10)", "Acceptable Answers": "(√5 - 1)/4"},
        {"Unacceptable Answers": "1/√3", "Acceptable Answers": "√3/3"},
        {"Unacceptable Answers": "61/31415", "Acceptable Answers": "1/515"},
        {"Unacceptable Answers": "Sin (π)", "Acceptable Answers": "0"},
    ];

    const contestPhotos = [
        "/3MT-2025/pics/im1.jpg",
        "/3MT-2025/pics/im2.jpg",
        "/3MT-2025/pics/im3.jpg",
        "/3MT-2025/pics/im4.jpg",
    ];
    const potentialTopicImages = [
        "/MMM/prevQuestions/im1.png",
        "/MMM/prevQuestions/im2.png",
        "/MMM/prevQuestions/im3.png",
        "/MMM/prevQuestions/im4.png",
        "/MMM/prevQuestions/im5.png",
    ];

    const topicsCovered = [
        { "Algebra": "<ul><li>Systems of equations</li> <li>Quadratics</li> <li>Vieta’s</li> <li>Binomial Theorem</li> <li>Radicals/Exponents</li> <li>Simon’s Favorite Factoring Trick</li> <li>Ratios</li> <li>(Infinite) Geometric Series</li> <li>Arithmetic Series</li> <li>Sum/Difference of Powers</li> <li>Rate/Time</li> <li>Floor/Ceiling</li> <li>Absolute Value</li> <li>Substitution (Nested Roots/Repeated Fractions)</li> <li>Mean, Median, Mode, Range</li> <li>Telescoping</li></ul>",
        "Combinatorics": "<ul><li>Sticks and Stones</li> <li>Permutation/Combination</li> <li>Properties of Inclusion Exclusion for three or less sets</li> <li>Basic Geometric Probability</li> <li>Conditional Probability</li> <li>Expected Values</li> <li>Complementary Counting</li> <li>Recursion</li> <li>Bijections</li> <li>Casework</li> <li>Pigeonhole Principle</li> <li>Double-counting</li> <li>Basic Invariants</li></ul>",
        "Geometry": "<ul><li>Area Formulas</li> <li>Volume Formulas</li> <li>Shoelace Formula</li> <li>Pythagorean Theorem</li> <li>Distance Formula</li> <li>Similar Triangles</li> <li>Angle Chasing</li> <li>Power of a Point</li> <li>Basic Mass Points</li> <li>Heron’s Formula</li> <li>Pick’s Theorem</li> <li>Surface Area for Pyramids, Prisms, and Cones</li> <li>Arcs and Sectors</li> <li>Angle Bisector Theorem</li> <li>Internal/External Angles</li></ul>",
        "Number Theory": "<ul><li>Fermat’s Little Theorem</li> <li>Euclidean Algorithm</li> <li>Chinese Remainder Theorem</li> <li>Divisibility</li> <li>Chicken McNugget Theorem</li> <li>GCD and LCM</li> <li>Number of Factors</li> <li>Sum of Factors</li> <li>Basic Modular Arithmetic</li> <li>Fundamental Theorem of Arithmetic</li></ul>" }
    ];

    const topicsSmall1 = [
        { "Algebra": "<ul><li>Systems of equations</li> <li>Quadratics</li> <li>Vieta’s</li> <li>Binomial Theorem</li> <li>Radicals/Exponents</li> <li>Simon’s Favorite Factoring Trick</li> <li>Ratios</li> <li>(Infinite) Geometric Series</li> <li>Arithmetic Series</li> <li>Sum/Difference of Powers</li> <li>Rate/Time</li> <li>Floor/Ceiling</li> <li>Absolute Value</li> <li>Substitution (Nested Roots/Repeated Fractions)</li> <li>Mean, Median, Mode, Range</li> <li>Telescoping</li></ul>",
        "Combinatorics": "<ul><li>Sticks and Stones</li> <li>Permutation/Combination</li> <li>Properties of Inclusion Exclusion for three or less sets</li> <li>Basic Geometric Probability</li> <li>Conditional Probability</li> <li>Expected Values</li> <li>Complementary Counting</li> <li>Recursion</li> <li>Bijections</li> <li>Casework</li> <li>Pigeonhole Principle</li> <li>Double-counting</li> <li>Basic Invariants</li></ul>" }
    ];
    const topicsSmall2 = [
        { "Geometry": "<ul><li>Area Formulas</li> <li>Volume Formulas</li> <li>Shoelace Formula</li> <li>Pythagorean Theorem</li> <li>Distance Formula</li> <li>Similar Triangles</li> <li>Angle Chasing</li> <li>Power of a Point</li> <li>Basic Mass Points</li> <li>Heron’s Formula</li> <li>Pick’s Theorem</li> <li>Surface Area for Pyramids, Prisms, and Cones</li> <li>Arcs and Sectors</li> <li>Angle Bisector Theorem</li> <li>Internal/External Angles</li></ul>",
        "Number Theory": "<ul><li>Fermat’s Little Theorem</li> <li>Euclidean Algorithm</li> <li>Chinese Remainder Theorem</li> <li>Divisibility</li> <li>Chicken McNugget Theorem</li> <li>GCD and LCM</li> <li>Number of Factors</li> <li>Sum of Factors</li> <li>Basic Modular Arithmetic</li> <li>Fundamental Theorem of Arithmetic</li></ul>" }
    ];
    const topicsAlgebra = [
        {"Algebra": "<ul><li>Systems of equations</li> <li>Quadratics</li> <li>Vieta’s</li> <li>Binomial Theorem</li> <li>Radicals/Exponents</li> <li>Simon’s Favorite Factoring Trick</li> <li>Ratios</li> <li>(Infinite) Geometric Series</li> <li>Arithmetic Series</li> <li>Sum/Difference of Powers</li> <li>Rate/Time</li> <li>Floor/Ceiling</li> <li>Absolute Value</li> <li>Substitution (Nested Roots/Repeated Fractions)</li> <li>Mean, Median, Mode, Range</li> <li>Telescoping</li></ul>"}
    ];
    const topicsCombo = [
        {"Combinatorics": "<ul><li>Sticks and Stones</li> <li>Permutation/Combination</li> <li>Properties of Inclusion Exclusion for three or less sets</li> <li>Basic Geometric Probability</li> <li>Conditional Probability</li> <li>Expected Values</li> <li>Complementary Counting</li> <li>Recursion</li> <li>Bijections</li> <li>Casework</li> <li>Pigeonhole Principle</li> <li>Double-counting</li> <li>Basic Invariants</li></ul>"}
    ];
    const topicsGeo = [
        {"Geometry": "<ul><li>Area Formulas</li> <li>Volume Formulas</li> <li>Shoelace Formula</li> <li>Pythagorean Theorem</li> <li>Distance Formula</li> <li>Similar Triangles</li> <li>Angle Chasing</li> <li>Power of a Point</li> <li>Basic Mass Points</li> <li>Heron’s Formula</li> <li>Pick’s Theorem</li> <li>Surface Area for Pyramids, Prisms, and Cones</li> <li>Arcs and Sectors</li> <li>Angle Bisector Theorem</li> <li>Internal/External Angles</li></ul>"}
    ];
    const topicsNT = [
        {"Number Theory": "<ul><li>Fermat’s Little Theorem</li> <li>Euclidean Algorithm</li> <li>Chinese Remainder Theorem</li> <li>Divisibility</li> <li>Chicken McNugget Theorem</li> <li>GCD and LCM</li> <li>Number of Factors</li> <li>Sum of Factors</li> <li>Basic Modular Arithmetic</li> <li>Fundamental Theorem of Arithmetic</li></ul>"}
    ];

    const testimonials = [
        {
            quote: "This is one of the best contests I did this year! It also was the longest, and I really liked the mystery puzzle!” ",
            author: "Leeoz Nebat",
            title: "Mustang Math Tournament Participant, Nevada 2025"
        },
        {
            quote: "It's a fun opportunity for the kids to work in teams.",
            author: "David Freeman",
            title: "MMT 2025 Coach, Northern California"
        }
    ];
</script>

<svelte:head>
	<title>MMM</title>
</svelte:head>

<svelte:window bind:innerWidth={windowWidth} />

<PageHeader
	title="MMM"
	description="Mustang Math Mania"
	button_url="https://docs.google.com/document/d/1KcXrzksrI2VY84erTJ4I1dNTMSxQ3ujXwqWMD3i8MUg/edit?tab=t.0#heading=h.i7gdx55nkvd8"
	button_text="Register Now"
	id="registerFor3MT"
/>

<Section>
    <br /> <br />
    <Heading text="What is MMM?" size={4} textColor="#1B9AAA" />
    <FlexBox>
        <PanelBox width="80%" style="min-width: 360px;">
            <p style="font-size: 1.2em; margin: 5px">
Mustang Math Mania is a middle school math competition run for students around the nation. It is put together by Mustang Math, a 501(c)(3) nonprofit organization made up of high school and college students!
<br><br>
The tournament is centered around teamwork and collaboration, incentivizing students to work with their teams not only to navigate the challenging but interesting problems of the tournament, but also to develop strategies to master the unique and fun game-like rounds. Kicking off the week prior to the tournament with a proof based round tailored towards middle school students, and continuing with innovative and interesting rounds such as “the ground is lava” and a risky gambling round, our tournaments are filled with fun and excitement for students at all levels. 
<br><br>
Don't believe us? Check out some comments from past participants below!
<br><br>
DATE: September 26th, 2026 <br>
TEAM SIZE: 3-4*<br>
LOCATION: Online<br>
EARLY EQUINE COST: $12 per participant (Register before September 5th, 2026)<br>
NORMAL COST: $15 per participant (Register before September 19th, 2026)<br>
LATE COST: $20 per participant (Register before September 22nd, 2026)<br>
<br><br>
<b><a href = "https://docs.google.com/document/d/1KcXrzksrI2VY84erTJ4I1dNTMSxQ3ujXwqWMD3i8MUg/edit?usp=drivesdk">Click Here To Access Registration Instructions</a></b><br>
<b><a href = "https://docs.google.com/document/d/1xAx_feHicQjdqq-PhWK8bF2HBch5pzpPzju9qhw7pOo/edit?usp=drivesdk">Click Here To Access Further Information</a></b><br>
<br><br>
*: Incomplete teams of 1-2 may be merged with other teams to make a full team of 3-4
            </p>
        </PanelBox>
    </FlexBox>
</Section>

<Section>
    <br /> <br />
    <Heading text="Intro to Proofs Seminar" size={3} textColor="#FF2E00" />
    <FlexBox>
        <PanelBox width="60%" style="min-width: 360px;">
            <p style="font-size: 1.2em; margin: 5px">
In addition to the competition itself, we are hosting 2 free Intro to Proofs classes to prepare students for the week-long proof round in MMM! Class 1 will cover logic and proof techniques like contradiction. Class 2 will be slightly more challenging and focus on induction. These classes will be a great opportunity to gain a head start and develop stronger mathematical foundations. Proof techniques, which aren’t covered in a typical middle school classroom will benefit both students with no proof experience and experienced problem solvers. If interested, please join the google classroom with the code <b>NMT3DOEW</b> (<b><a href = "https://classroom.google.com/c/ODg0NzE4OTc2ODU5?cjc=nmt3doew">Google Classroom Link</a></b>).
            </p>
        </PanelBox>
    </FlexBox>
</Section>

<Section>
    <br /> <br />
    <Heading text="Registration Details" size={3} textColor="#1B9AAA" />
    <div>
        <Heading text="Schedule" size={2} textColor="#1B9AAA" />
        <div class="schedule-wrapper">
            <FlexBox>
                <PanelBox>
                    <Table data={scheduleData} width="auto" headerColor="#1B9AAA" rowColors={["#A4D6AF", "#ADCDD6"]} cellPadding={5} cellPaddingRight={20}/>
                    <p style="font-size: 0.9em; text-align: center; margin-top: 10px; font-style: italic;">
                        *Schedule subject to change. Note that there is built-in buffer time to explain instructions & assist with technical difficulties.
                    </p>
                </PanelBox>
            </FlexBox>
        </div>
    </div> <br />
    <div>
        <Heading text="Awards" size={2} textColor="#1B9AAA" />
        <FlexBox>
            <p style="font-size: 1.2em; margin: 5px">We will be awarding the top teams of each division with <p1 style="color: red">$25 Amazon Gift Cards!</p1></p>
        </FlexBox>
    </div>
    <Dropdown mainText="Rules">
        <p1 style="font-size: 1.2em; margin: 5px">
<Heading text = "General Rules" size = {1} textColor="#1B9AAA"></Heading>
No Cheating - This contest has a zero-tolerance cheating policy. Any evidence of cheating may lead to immediate disqualification, or any other punishment deemed appropriate by competition staff.
<br><br>
<ul>
    <li>No calculators, rulers, compasses, protractors, or other aids are permitted.</li>
    <li>You may not use the Internet or AI tools (e.g. ChatGPT) as a resource at any point during a test.
        <ul>
            <li>We may require individuals to provide a solution for a problem during the competition - so keep track of your work!</li>
        </ul>
    </li>
    <li>Team divisions are determined by the highest grade level amongst the team members
    <ul>
        <li>Eg: Teams with 1 or more 8th graders will be in the Stallion division, teams with 7th graders and below will be in the Colt division, and teams with 6th graders and below will be in the Foal division. </li>
        <li>Teams may choose to compete in a higher division, but may not compete in a lower division.</li>
    </ul>
    </li>
</ul>

<Heading text = "Answer Formatting Rules" size = {1} textColor="#1B9AAA"></Heading>
<ul>
    <li>Make sure you don’t have any extra calculations in your answers!</li>
    <li>For example, 78 and 2<sup>85</sup> is okay, but ½ + ⅓ is not. 
    Simplify radicals!</li>
    <li>Rewrite expressions like √63 into 3√7 and √(1/9) as ⅓ (exact decimal answers are also acceptable)</li>
    <li>Rationalize all denominators - write 1/√2 as √2/2 and 1/(√2 - 1) as √2 + 1</li>
    <li>No repeating sums / products!</li>
    1.333… should be submitted as 4/3 and 2*2*2*2*2 as 32
    <li>If you have any further questions, please contact us at <Link target="_blank" url="mailto:tournament@mustangmath.com" text="tournament@mustangmath.com" />!</li>
</ul>

        </p1>
        <div class="acceptable-wrapper">
            <FlexBox>
                <PanelBox>
                    <Table data={acceptableData} width="auto" headerColor="#1B9AAA" rowColors={["#A4D6AF", "#ADCDD6"]} cellPadding={5} cellPaddingRight={20}/>
                </PanelBox>
            </FlexBox>
        </div>
    </Dropdown>
    <Dropdown mainText="Rounds">
        <Heading text = "Proof Round" size = {1} textColor="#1B9AAA"></Heading>
        <p style="font-size: 1.2em; margin: 5px">The week before competition day, teams will compete in a proof-writing competition. This round will consist of various problems in which students must either compute an answer, explain their reasoning, or write mathematically sound proofs to demonstrate why some property holds true.</p>
        
        <Heading text = "Solo Stampede" size = {1} textColor="#1B9AAA"></Heading>
        <p style="font-size: 1.2em; margin: 5px">Students will compete individually to answer a 25 question test in 60 minutes. These individual scores will be factored into the team score at the end.</p>
        
        <Heading text = "Meltdown Madness" size = {1} textColor="#1B9AAA"></Heading>
        <p style="font-size: 1.2em; margin: 5px">Teams will compete in a 25 question test over 50 minutes. After the first minute, problem #1 will sink and become unsolvable. Every minute, the next problem will sink until all 25 problems become locked (new answers can not be submitted). Students will only earn points on unlocked problems solved correctly.</p>

        <Heading text = "Betting Bonanza" size = {1} textColor="#1B9AAA"></Heading>
        <p style="font-size: 1.2em; margin: 5px">Teams start with 100 points and 5 problem sets, each with a multiplier, (1.5, 2, 2.5, 3, and 3.5). Teams can then bet/allocate their points to sets before seeing problems, keeping any unused points. Over the next 45 minutes, teams work to solve the 25 problems. Each full set correctly solved returns the bet points multiplied, no points otherwise. Teams also earn 2 bonus points per correct problem, with a maximum of 50 bonus points.</p>
    </Dropdown>
    <Dropdown mainText="Potential Topics Covered">
        {#if windowWidth > 1000}
            <Table data={topicsCovered} width="100%" headerColor="#1B9AAA" rowColors={["#A4D6AF"]} cellPadding={5} cellPaddingRight={20} textSize={1} cellStyle="vertical-align: top; font-size: {windowWidth/1200}em;" tableStyle="table-layout: fixed; padding: 10px;" headerStyle="font-size: {windowWidth/1500}em;" />
        {:else if windowWidth > 800}
            <Table data={topicsSmall1} width="100%" headerColor="#1B9AAA" rowColors={["#A4D6AF"]} cellPadding={5} cellPaddingRight={20} textSize={1} cellStyle="vertical-align: top; font-size: {windowWidth/800}em;" tableStyle="table-layout: fixed; padding: 10px;" headerStyle="font-size: {windowWidth/800}em;" />
            <Table data={topicsSmall2} width="100%" headerColor="#1B9AAA" rowColors={["#A4D6AF"]} cellPadding={5} cellPaddingRight={20} textSize={1} cellStyle="vertical-align: top; font-size: {windowWidth/800}em;" tableStyle="table-layout: fixed; padding: 10px;" headerStyle="font-size: {windowWidth/800}em;" />
        {:else}
            <Table data={topicsAlgebra} width="100%" headerColor="#1B9AAA" rowColors={["#A4D6AF"]} cellPadding={5} cellPaddingRight={20} textSize={1} cellStyle="vertical-align: top; font-size: {windowWidth/500}em;" tableStyle="table-layout: fixed; padding: 10px;" headerStyle="font-size: {windowWidth/500}em;" />
            <Table data={topicsCombo} width="100%" headerColor="#1B9AAA" rowColors={["#A4D6AF"]} cellPadding={5} cellPaddingRight={20} textSize={1} cellStyle="vertical-align: top; font-size: {windowWidth/500}em;" tableStyle="table-layout: fixed; padding: 10px;" headerStyle="font-size: {windowWidth/500}em;" />
            <Table data={topicsGeo} width="100%" headerColor="#1B9AAA" rowColors={["#A4D6AF"]} cellPadding={5} cellPaddingRight={20} textSize={1} cellStyle="vertical-align: top; font-size: {windowWidth/500}em;" tableStyle="table-layout: fixed; padding: 10px;" headerStyle="font-size: {windowWidth/500}em;" />
            <Table data={topicsNT} width="100%" headerColor="#1B9AAA" rowColors={["#A4D6AF"]} cellPadding={5} cellPaddingRight={20} textSize={1} cellStyle="vertical-align: top; font-size: {windowWidth/500}em;" tableStyle="table-layout: fixed; padding: 10px;" headerStyle="font-size: {windowWidth/500}em;" />
        {/if}
        <br />
        <Heading text="Sample Questions" size={1} textColor="#1B9AAA"></Heading>
        <SlideshowNew images={potentialTopicImages}></SlideshowNew>
    </Dropdown>
    <Dropdown mainText="FAQ">
        <div style="margin-left: 5vw; margin-right: 5vw; font-size: 1.1em;">
            <p>
                <strong>Q:</strong> I'm a parent or a student, not a coach - how can I register? <br />
                <strong>A:</strong> Mustang Math doesn't require you to be a coach! A parent can act as a coach (and register as a coach on ContestDojo) to create an organization and team(s) for their participating students. <strong>Students should not create coach accounts.</strong>
            </p>
            <p>
                <strong>Q:</strong> Why aren't there awards for high schoolers? <br />
                <strong>A:</strong> Our mission and tests are geared towards middle school mathematics, and thus our awards are as well. We welcome high school students to participate for the experience only.
            </p>
            <p>
                <strong>Q:</strong> You have three divisions, what are the differences? <br />
                <strong>A:</strong> Our Foal Division is for students in 6th grade and below, Colt Division is for 7th grade, and Stallion Division is for 8th grade. Students may compete in divisions higher than their grade level but are not allowed to compete in lower divisions.
            </p>
            <p>
                <strong>Q:</strong> Where can I find practice material for the tests? How can we prepare? <br />
                <strong>A:</strong> You can take a look at our <a target="_blank" sveltekit:prefetch href="/past-tests">past tests</a>, and we also highly recommend looking at <a target="_blank" sveltekit:prefetch href="https://www.mathcounts.org/resources/past-competitions">past MathCounts</a>, <a target="_blank" sveltekit:prefetch href="https://artofproblemsolving.com/wiki/index.php/AMC_Problems_and_Solutions">AMC 8/10</a>, and <a target="_blank" sveltekit:prefetch href="https://www.ocf.berkeley.edu/~bmt/archive/">BmMT</a> tests as these are similar in level to the problems at MMT.
            </p>
            <p>
                <strong>Have more questions?</strong> Please feel free to contact us at <Link target="_blank" url="mailto:tournament@mustangmath.com" text="tournament@mustangmath.com" />!
            </p>
        </div>
    </Dropdown>
</Section>

<Section>
    <div class="split-layout">

        <div class="column">
            <Heading text = "Past Contest Photos" size = {2} textColor="#1B9AAA"></Heading>
            <SlideshowNew images={contestPhotos} />
        </div>

        <div class="column">
        
        <div class="testimonials-section">
            <Heading text = "What people are saying" size = {2} textColor="#1B9AAA"></Heading>
            <p1>Collective testimonials for Mustang Math's competitions</p1><br><br>
            {#each testimonials as testimonial}
            <div class="testimonial">
                <p class="quote">"{testimonial.quote}"</p>
                <p class="author">- {testimonial.author}, {testimonial.title}</p>
            </div>
            {/each}
        </div>
    </div>
</div>
</Section>

<br><br><br><br><br>

<style>
.split-layout {
display: flex;
flex-wrap: wrap; /* Allows columns to stack on smaller screens */
gap: 30px; /* Space between the two columns */
}

.column {
flex: 1; /* Each column will take up equal space */
min-width: 300px; /* Ensures columns don't get too squished before wrapping */
}


/* Testimonial Styles */
.testimonial {
background-color: #f9f9f9;
padding: 20px;
border-radius: 8px;
margin-bottom: 20px;
border-left: 4px solid #ddd;
max-width: 800px;
}

.testimonial .quote {
font-style: italic;
color: #555;
margin-bottom: 10px;
}

.testimonial .author {
font-weight: bold;
text-align: right;
color: #333;
}

/* Responsive behavior for smaller screens */
@media (max-width: 768px) {
.split-layout {
    flex-direction: column; /* Stack columns vertically */
}
}

</style>
