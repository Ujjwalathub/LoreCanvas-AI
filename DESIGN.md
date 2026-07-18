# 📌 Living Lore Board — Skeuomorphic Frontend Design Document

> **Theme:** Premium Skeuomorphism
> **Stack:** React 18 + TypeScript + Vite + Tailwind CSS + Framer Motion  
> **Backend:** FastAPI
> **Aesthetic:** Realistic Corkboard, Tactile Cards, Tangible UI, High-End Professional

---

## 1. Project Overview & Visual Identity

**Living Lore Board** is a highly interactive, AI-powered tool for storytellers, game masters, and authors. It allows users to build dynamic knowledge graphs representing the complex relationships in their fictional worlds. 

### Visual Concept (Premium Skeuomorphism)
To ground the user in a tactile, natural experience, the frontend will adopt a **Premium Skeuomorphism** design. This design language mimics real-world physical objects—bringing the "messy corkboard" to life but with pristine, high-end finishing. 

Instead of flat, abstract UI, users will interact with:
- **Rich Cork Textures:** The main canvas is a highly detailed, warmly-lit corkboard.
- **Physical Cards:** Lore nodes are represented as textured paper cards pinned to the board.
- **Realistic Pushpins & Strings:** The connections between characters will look like real red or purple strings wrapped around physical pushpins with metallic sheens and soft drop-shadows.

![Skeuomorphic Corkboard UI Concept](./assets/skeuomorphic_corkboard.png)
*Concept: The Living Lore Board displaying pinned character cards with realistic textures, pushpins, and connecting strings.*

---

## 2. Outstanding Features & Required UI Elements

Based on the current frontend implementation, the application provides a robust suite of tools organized into a tactical sidebar (with 5 dedicated tabs) and an interactive canvas.

### 📌 The Interactive Corkboard (Main Canvas)
- **Fluid Drag-and-Drop:** Built on React Flow, cards (entities) can be freely dragged and arranged on the corkboard. 
- **Entity Categorization:** Nodes are color-coded (Character: Amber, Location: Emerald, Organization: Blue, Event: Rose). In the skeuomorphic design, these will translate to differently colored physical pushpins or ribbon tags.
- **Dynamic Minimap & Navigation:** A floating minimap (styled like a small clipboard map) allows for seamless panning and zooming across the vast corkboard.
- **String Connections:** Drawing an edge between two cards automatically triggers a request to the backend to generate lore explaining their connection. Up to 6 entities can be "pinned" together at once for complex relationship weaving.

### ➕ Add Node Panel (Manual Creation)
- **Direct Entry:** Allows users to manually create new character, location, organization, or event cards and pin them directly to the board.

### 📜 Lore Generation Panel (Gemini 1.5 Flash)
- **Story Generation:** When entities are connected via string, the AI generates a multi-paragraph backstory explaining their relationship. 
- **Parchment Display:** The generated story is presented in a "Typewriter" styled dialog box or piece of "parchment" paper, maintaining the illusion of compiling an ancient tome.

### 🎨 Avatar Generation Panel (FLUX.1-schnell)
- **Polaroid/Card Avatars:** When a user selects a Character node, they can generate a high-quality portrait that attaches to the node like a freshly printed Polaroid or hand-painted miniature.
- **In-Canvas Integration:** Portraits instantly update the node card on the board, visually enriching the world graph.

### 🧠 Smart Reading & Entity Extraction (BERT NER)
- **Prose Import:** Users can paste bulk text (up to 512 characters) into a "Notebook" panel (styled as a leather-bound journal).
- **Smart Deduplication & Bulk Add:** The system extracts nouns, groups them by entity type, and provides a checklist. It automatically grays out entities that are already on the board to prevent duplicates, allowing the user to bulk-add the rest with a single click.
- **Detailed Inspection:** A side-pane allows users to inspect individual extracted entities before pinning them to the board.

### 🕰️ History & Session Log Panel
- **Chronological Archive:** Maintains a complete session history of all generated lore connections (saved locally via Zustand persist).
- **Lore Recall:** Users can review previously generated stories and connections in a chronological scroll, acting as a permanent record of their world-building session.

---

## 3. UI & Design System

### Materials & Colour Palette

| Element | Material/Hex | Usage |
|---|---|---|
| **Canvas Base** | High-Res Cork Texture | The main background for the lore board |
| **Card Surface** | Textured Off-White (`#fcfaf2`) | The paper cards representing nodes |
| **Pushpins** | Metallic & Ruby Red | Anchors for the cards and strings |
| **Strings** | Woven Thread Texture | The connections (edges) between nodes |
| **Ink/Text** | Deep Charcoal (`#2b2b2b`) | Primary text on the paper cards |
| **Accents** | Brass & Leather (`#8c5a2b`) | Used for menus, sidebars, and buttons |

### Typography

- **UI & Menus:** *Inter* or *Roboto* (Clean, modern contrast for the surrounding app frame).
- **Card Titles & Lore Text:** *Courier Prime*, *Special Elite*, or *Playfair Display* (Simulating typewriter text or elegant handwriting on the cards).

### Micro-Animations & Interactions
- **Hover States:** Hovering over a card slightly increases its drop-shadow, making it feel like it's lifting off the corkboard.
- **String Tension:** When dragging a connected card, the connecting string dynamically adjusts its tension, curving slightly before pulling taut.
- **Pinning Action:** A sharp, satisfying animation of a pin pressing into the board when a new card is dropped.

---

## 4. Component Architecture

```text
<AppShell>
  <WoodenFrameHeader />
  <main>
    <JournalSidebar className="leather-texture">
      <TabBar /> (Embossed tabs)
      <Panels /> (Add Node, Lore, Avatar, Extract, History)
    </JournalSidebar>
    <CorkboardCanvas>
      <CorkBackground />
      <PaperCardNode /> (Rounded corners, paper texture, pushpin graphic)
      <ThreadEdge /> (Textured curved line with shadow)
    </CorkboardCanvas>
  </main>
</AppShell>
```

---

## 5. Implementation Roadmap

1. **Setup & Assets:** Gather high-resolution textures (cork, paper, leather) and import them into Vite/Tailwind.
2. **Skeuomorphic Graph (React Flow):** Customize the `LoreNode` to render as a paper card with a pin, and `LoreEdge` to render as a drop-shadowed string.
3. **Sidebar & Tools:** Build the `JournalSidebar` and integrate it with the main app state.
4. **API Integration:** Connect the frontend to the FastAPI backend, ensuring generated avatars fit seamlessly onto the polaroid-style cards.
5. **Polish & Physics:** Add Framer Motion for tactile hover effects and transitions. Ensure drop-shadows have realistic directional lighting.
