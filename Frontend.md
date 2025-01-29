## Block Builder for Content Items

- Located in `components/common/ContentEditor`
- **Block Types:** Defined in `components/common/ContentEditor/blocktypes.ts`
- **Block Components:** Defined in `components/common/ContentEditor/blocks/`

### Text Editor: TipTap

- Used as the text editor in the block builder.
- **TipTap Extensions Used:**
  - StarterKit
  - Placeholder
  - TextStyle
  - FontFamily
  - Underline
  - Color
  - TextAlign
  - FontSize
  - LineHeight
- **Main TipTap Editor Component:** Defined in `components/common/inputs/`
- **Menu Bar for Editor:** Defined in `components/common/TipTap/MenuBar/MenuBar`

### UI Components: ArkUI

Used for accordion, carousel, and tabs in block builder:

- Accordion
- AccordionContent
- AccordionItem
- AccordionTrigger
- Editable
- EditableArea
- EditableInput
- EditablePreview
- ColorPicker

---

## Miscellaneous Notes

- `on_fly` in `UserContents` should be removed **(Check if it is used first—it shouldn't be?)**
- `CreateCourse` mutation is **not in its own hook?**

---

## Authenticating with AWS using GitHub Actions

- Reference: [AWS IAM Roles for GitHub Actions](https://aws.amazon.com/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws/)
