<script>
    import PageHeader from '$lib/components/PageHeader.svelte';
    import Section from '$lib/components/Section.svelte';
    import Heading from '$lib/components/Heading.svelte';
    import FlexBox from '$lib/components/FlexBox.svelte';
    import Image from '$lib/components/Image.svelte';
    import PanelBox from '$lib/components/PanelBox.svelte';
    import Link from '$lib/components/Link.svelte';
    import sponsorTiers from '$lib/jsons/sponsorTiers';

    let windowWidth;
    let windowHeight;
    let learnMoreIsVisible = true;
    let y;
    let scrollOpacity = 1;
    $: scrollOpacity = Math.max((windowHeight - 2 * y) / windowHeight, 0);
    $: learnMoreIsVisible = scrollOpacity > 0;

    function scrollToElem(e) {
        e.scrollIntoView({
            behavior: "smooth",
        });
    }
</script>

<svelte:window
    bind:scrollY={y}
    bind:innerWidth={windowWidth}
    bind:innerHeight={windowHeight}
/>

<svelte:head>
	<title>Partners and Sponsors</title>
</svelte:head>

<PageHeader title="Partners & Sponsors" description="The Organizations Making MM Possible" button_url="
https://drive.google.com/file/d/1WubRiqJ7TAcbwGY8PX-xHiY5-_1r7iS3/view" button_text="Sponsor Mustang Math!" button_id="sponsorMM"/>



<Section>
    <br /> <br />
    <Heading text="Sponsors and Partners" size={4} textColor="#1B9AAA" />
    <FlexBox>
        <PanelBox width="60%" style="min-width: 360px;">
            <p style="font-size: 1.2em; margin: 5px">Thank you to our sponsors and partners for supporting the Mustang Math Tournament and our vision of providing a fun, collaborative team competition to motivated and bright middle school students!<br><br>
            Interested in sponsoring or partnering? Check out our <b><a href = https://tinyurl.com/MMSponsors2024>sponsorship packet</a></b> and reach out to us at <Link target="_blank" url="mailto:contact@mustangmath.com" text="contact@mustangmath.com" />.
            All sponsorships are used to help fund our competitions, classes, and other activities and improving the quality of such events.</p>
        </PanelBox>
    </FlexBox>
</Section>

{#each sponsorTiers as lvl}
    <Section>
        <br /> <br />
        <Heading text="{lvl.name}" size={3} textColor={lvl.headerColor} />
            <FlexBox wrap={true} align="stretch">
                {#if lvl.sponsors.length > 0}
                    {#each lvl.sponsors as sponsor}
                        <PanelBox borderRadius="20px" width="40%" style="max-width: 300px; min-height: 250px; min-width: 250px;">
                            <a target="_blank" href={sponsor.link} style="height: 100%; display: flex; align-items: center;text-decoration:none;">
                                <div>
                                    <img src={sponsor.url} alt={sponsor.alt} style="max-width: 100%;">
                                    {#if sponsor.blurb}
                                        <p style="font-size: 11px; text-align: center;">{sponsor.blurb}</p>
                                    {/if}
                                </div>
                            </a>
                        </PanelBox>
                    {/each}
                {:else}
                    <p>Become our first {lvl.singular}!</p>
                {/if}
            </FlexBox>
    </Section>
{/each}
<style>
    
</style>
