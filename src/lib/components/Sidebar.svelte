<script>
    import { onMount, afterUpdate } from 'svelte';
  
    let sections = []; // Array to store section details
    let expanded = false; // Boolean to track sidebar expansion
    let currentSection; // Variable to store current section ID
  
    // Function to toggle sidebar expansion
    function toggleSidebar() {
      expanded = !expanded;
    }
  
    // Function to scroll to a section
    function scrollToSection(id) {
      const section = document.getElementById(id);
      section.scrollIntoView({ behavior: 'smooth' });
    }
  
    // Function to update current section based on scroll position
    function updateCurrentSection() {
      const scrollPosition = window.scrollY;
      for (let i = sections.length - 1; i >= 0; i--) {
        if (scrollPosition >= sections[i].offsetTop) {
          // Set current section
          currentSection = sections[i].id;
          break;
        }
      }
    }
  
    onMount(() => {
      updateSectionsArray();
      // Listen for scroll events to update current section
      window.addEventListener('scroll', updateCurrentSection);
  
      // Initial calculation of current section
      updateCurrentSection();
  
      // Cleanup scroll event listener on component destroy
      return () => {
        window.removeEventListener('scroll', updateCurrentSection);
      };
    });
  
    // Update sections array after DOM updates
    afterUpdate(() => {
      updateSectionsArray();
    });
  
    // Function to update the sections array
    function updateSectionsArray() {
      sections = Array.from(document.querySelectorAll('section')).map(section => ({
        id: section.id,
        offsetTop: section.offsetTop
      }));
    }
  </script>
  
  <style>
    .sidebar {
      position: fixed;
      top: 50%;
      transform: translateY(-50%);
      right: -100px; /* Initially hide the sidebar */
      background-color: #fff;
      border: 1px solid #ccc;
      padding: 10px;
      transition: right 0.3s ease;
    }
  
    .sidebar:hover {
      right: 0; /* Show the sidebar on hover */
    }
  
    .section-link {
      display: block;
      margin-bottom: 5px;
      cursor: pointer;
    }
  </style>
  
  <div class="sidebar" on:mouseleave={toggleSidebar}>
    {#if expanded}
      {#each sections as section}
        <div class="section-link" on:click={() => scrollToSection(section.id)}>
          {section.id}
        </div>
      {/each}
    {:else}
      <div class="section-link" on:click={() => scrollToSection(currentSection)}>
        {currentSection}
      </div>
    {/if}
  </div>
  